# General Concerns

## Worker model

By default, webservice starts with 1 **worker**. 
Each worker process documents in a **single-threaded** mode, that mean can process only **one** request at a time.
So if you submit many requests at once they will queue up and will be processed one by one.

For improved throughput performance you need to launch more workers according to the planned load.
Webservice can spawn **multiple** workers under **one** service instance.
You may set workers number based on the [hardware limitation](#prerequisites) you have.
Also, you can use **N** webserver instances with **multiple** workers under loadbalancer to increase performance even father.

{% hint style="warning" %}
**Each worker** in our license model counts as **instance**. 
Thus, setup - 3 machines with 2 workers on each - **requires** a license with 6 instances. 

For **transaction-based** licenses number of workers is not limited,
only amount of **process requests**  counts.
{% endhint %}

## Proxy Guard

**Regula Document Reader** is **not** general HTTP webserver, that handles hundreds of request per second.
Typical document processing takes up to a few seconds, so we can call it CPU intensive.
Considering that typical instance has 1-4 workers, we need to carefully manage workers time. 
One of the main sources of **waisting** worker's processing time is **slow clients** problem.
When webservice receives request from client with a **slow** internet connection,  
free worker start receiving that request. 
The worker will be bottlenecked by the speed of the client connection, 
and it will be blocked **until** the slow client finishes sending large ID image.
Being blocked means that this worker process can not handle any other request in the meantime, 
it’s just there, **idle**, waiting to receive the entire request, so it can start really processing it.

We strongly recommend using **Regula Document Reader** behind a proxy server.
Although there are many HTTP proxies available, we strongly advise that you use Nginx. 
If you choose another proxy server, you need to make sure that it buffers slow clients.

{% hint style="danger" %}
Typical Load Balancers from cloud provides, such as ELB/ALB from aws, 
do **not** buffer slow clients. 
So you **still need** to use some **proxy** server between LB and **Regula Document Reader**.
{% endhint %}

## Prerequisites

Recommended machine settings: 1CPU and 2Gb RAM per worker.

{% hint style="warning" %}
For using docker / Linux instances you will need an **Online** license.
Internet connection is a mandatory requirement for an **Online** license, 
  thus the instance with pre-installed service must have internet access at least to 
  [**https://lic.regulaforensics.com/**](https://lic.regulaforensics.com/) URL.
{% endhint %}

## Versioning

The Version `A.B.C.D` is composed of:

* Regula SDK version `A.B`
* Document database version `C`
* Service wrapper version `D`

An example of version **5.2.103350.140** can be interpreted as:

* the Regula SDK version is `5.2`
* the current document database version is `103350`
* the webservice wrapper version is `140`

