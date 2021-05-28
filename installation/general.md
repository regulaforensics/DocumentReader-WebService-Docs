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

