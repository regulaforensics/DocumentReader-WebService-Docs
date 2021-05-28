# Quick Start Guide

## Prerequisites

* Recommended HW settings: 1CPU / 2Gb per worker
* **Internet connection is a mandatory requirement for an "On-line**" **license**, thus the instance with pre-installed service must have internet access at least to [**https://lic.regulaforensics.com/**](https://lic.regulaforensics.com/) URL.

## Versioning

The Version `A.B.C.D` is composed of:

* Regula SDK version `A.B`
* Document database version `C`
* Service wrapper version `D`

An example of version **5.2.103350.2** can be interpreted as:

* the Regula SDK version is `5.2`
* the current documents database version is `103350`
* the service wrapper version is `2`

## Service health check

Ensure the installed service is up and running.

Service availability can be checked at the following link [`http://localhost:8080/api/ping`](http://localhost:8080/api/ping)

Here you can find all the necessary license information/status and service version.

![](https://img.regulaforensics.com/Web/response.png)

