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

## Custom Options

Custom options can be set in two ways:

1. Environment variables
2. Using .env file

{% tabs %}
{% tab title="Linux" %}
```text
/opt/regula/document-reader-webapi/.env
```
{% endtab %}

{% tab title="Windows" %}
```text
%PROGRAMFILES%\Regula\Document Reader Web API\.env
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Environment variables take precedence over the .env file
{% endhint %}



* **DOCREADER\_BIND**: the bind ip\_address:port, default **0.0.0.0:8080**
* **DOCREADER\_BACKLOG**: the maximum number of requests in a queue, default **20**
* **DOCREADER\_WORKERS**: the number of workers to process requests, default **1**
* **DOCREADER\_LOG\_LEVEL**: the granularity of Error log outputs, default **info**, possible options **debug, info, warning, error, critical**
* **DOCREADER\_LOG\_FILE**: the absolute path to the Error log file to write to, default **-** \(log to stderr\)
* **DOCREADER\_ACCESS\_LOG\_FILE**: the absolute path to the Access log file to write to, default **-** \(log to stdout\)
* **DOCREADER\_LIC\_URL**: The URL to regula.license file for further download, if the mount option is not available, default **None** \(low priority over a mounted file\)
* **DOCREADER\_CERT\_FILE**: the absolute path to SSL certificate file
* **DOCREADER\_KEY\_FILE**: the absolute path to SSL key file
* **DOCREADER\_CORS\_ORIGINS**: allowed cors origins, default **same-origin policy**
* **DOCREADER\_CORS\_METHODS**: allowed cors methods, default **all methods**
* **DOCREADER\_CORS\_HEADERS**: allowed cors headers, default **all headers**

