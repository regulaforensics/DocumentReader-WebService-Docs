# Deployment

## Proxy Guard

**Regula Document Reader** is **not** general HTTP webserver, that handles hundreds of request per second. Typical document processing takes up to a few seconds, so we can call it CPU intensive. Considering that typical instance has 1-4 workers, we need to carefully manage workers time. One of the main sources of **waisting** worker's processing time is **slow clients** problem. When webservice receives request from client with a **slow** internet connection, free worker start receiving that request. The worker will be bottlenecked by the speed of the client connection, and it will be blocked **until** the slow client finishes sending **large** ID image. Being blocked means that this worker process can **not** handle any other request in the meantime, it’s just there, **idle**, waiting to receive the entire request, so it can start really processing it.

We strongly recommend using **Regula Document Reader** behind a proxy server. Although there are many HTTP proxies available, we strongly advise that you use **Nginx**. If you choose another proxy server, you need to make sure that it buffers slow clients.

{% hint style="danger" %}
Typical Load Balancers from cloud provides, such as ELB/ALB from aws, do **not** buffer slow clients. So you **still need** to use some **proxy** server between LB and **Regula Document Reader**.
{% endhint %}

## Health check and requests queue size

Configuring applications health check is not a trivial topic. Our **webservice** behaviour makes this topic even more nuanced. From one side, it's simple as querying one HTTP endpoint [`http://localhost:8080/api/ping`](http://localhost:8080/api/ping), which produces simple json output:

```javascript
{
  "app-name": "Regula Document Reader Web API",
  "license-id": "00000000-0000-0000-0000-000000000000",
  "license-serial": "OL00000",
  "server-time": "2021-06-28 09:16:00.453891+00:00",
  "valid-until": "2022-12-31T00:00:00Z",
  "version": "5.6.128414.450"
}
```

However, there are a few factors, that can cause a group of sequential checks to fail. One of the most faced issue of our customers is overload on peak times. Consider next scenario:

1. A webserver with one worker under load balancer 
2. A webserver backlog is 20 requests, load balancer perform health check every 30s with timeout of 30s
3. 20 request come in, 3 of them contain bad image of document, that will extend processing to 5sec 
4. Health check request comes in and gets queued \(as 21st request\)
5. To process the first 20 requests, server need `17 x 1 + 3 x 5=32` sec.
6. After a while, the health check caller \(load balancer\) times out
7. Load balancer thinks your application is broken, marking the instance broken, terminating it or stop routing requests

That can happen for any number of web servers under a load balancer. A host with overload is terminated, giving other hosts more requests, causing them to timeout health checks and get released too. To fix that, we have next options \(or combination of them\):

1. Increase health check timeout to 60s or even higher. Thus, we trade off for time to discover for really stacked nodes. If a webserver on a given node is crashed, that health check will fail fast with connection error. 
2. Decrease backlog size to 10 request and let requests from a load balancer fail, trigger a load balancer to shift traffic to another instance earlier. In general, use next empirical formula `health check timeout / 3` to determine desired backlog size.
3. Increase the number of consecutive health check fails required to trigger a load balancer to remove node from routing.
4. Increase health check period to 60s or even higher. Thus, if spike in load is not constant, server have more time to free backlog before queue health check.

