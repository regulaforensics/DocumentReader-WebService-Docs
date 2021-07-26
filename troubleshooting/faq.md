---
description: >-
  This section contains frequently asked questions and solutions to common
  issues related to Regula Web API.
---

# FAQ

Please review this page carefully before contacting our support team. 

**Please note: If you haven't found a solution and** [**need technical support**](mailto:support@regulaforensics.com)**, describe the issue as detailed as possible, including the steps you took to solve or reproduce it. Also please provide the log file, which can be found in the Web API installation directory. This will help us to find and fix the issue. Thank you!**

## Where can I download the latest Web API version?

Please use the [Regula Download Manager](https://support.regulaforensics.com/hc/en-us/articles/115004219343-Regula-Downloads-Manager) tool.

tbd

## How to change the service base address

tbd

## How to run the Web API service using HTTPS?

#### Option 1. Recommended. Nginx as a reverse-proxy

Run Nginx as a frontend container for HTTPS processing and proxy service requests to the backend docreader container. [link](https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/)

#### Option 2. Docreader via HTTPS

To run the docreader service via HTTPS:

* add 644 permissions to certificates so the server is able to read certificates
* pass cert.crt & cert.key files to the container
* pass DOCREADER\_CERT\_FILE, DOCREADER\_KEY\_FILE environment variables
* forward container port to 8443 host port

```text
chmod 644 ~/cert.crt ~/cert.key
```

```text
docker run -it -p 8443:8080 -v ~/regula.license:/app/extBin/unix_x64/regula.license -v ~/cert.crt:/app/cert.crt -v ~/cert.key:/app/cert.key -e DOCREADER_CERT_FILE="/app/cert.crt" -e DOCREADER_KEY_FILE="/app/cert.key" regulaforensics/docreader
```

## Documents are not recognized or recognized incorrectly

1. Check that you have the latest versions of SDK and document database installed
2. Make sure that the document image meets our [quality requirements](https://docs.regulaforensics.com/home/faq/image-quality-requirements)
3. Please send the incorrectly recognized document sample to [our support team](mailto:support@regulaforensics.com)

## How to recognize multi-page documents

You should submit both document pages within a single transaction as in the example below. Please, mark every separate page image with a different page index value. The transaction will be processed as usual. When the results are ready, the XML or JSON structure will contain a list with the results in accordance witn the requested result type \(for each page\).

```text
[ 
    {   "Base64ImageString": "base64 string", 
        "Format": ".jpg", 
        "LightIndex": 6, 
        "PageIndex": 0 
    },
    {   "Base64ImageString": "base64 string", 
        "Format": ".jpg", 
        "LightIndex": 6, 
        "PageIndex": 1
     } 
 ] 
```

## Where can I find logs?

## Is there a sample client available?

## Why do I get a 'null' or "Result of this type is not available" response?

1. Make sure that the image meets our [quality requirements](https://app.gitbook.com/@regulaforensics/s/home/faq/image-quality-requirements)
2. Check if the document you submitted actually contains the requested result type

## Error "Processing timeout". How to increase the maximum document processing time

## What capabilities value do you use on api.regulaforensics.com?

The default capabilities value used on the demo website api.regulaforensics.com is **500.** It includes MRZ, Visual Zone OCR, Document Type, Visual Graphics and Barcode Processing.

