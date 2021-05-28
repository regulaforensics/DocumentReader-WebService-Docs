# Changelog

## April 5, 2021 - v5.5

* Added _CERT\_FILE_ and _KEY\_FILE_ environment variables handling to obtain an external SSL certificate and private key for enabling HTTPS.
* Added pass-back object: if included in the request as “_passBackObject_” JSON object will be returned in response the same way.
* Fixed issue with missing write to folder permissions for request logging on start-up.
* Fixed issue with translating old-style API request capabilities value into scenario value.
* Fixed issue with non-ASCII characters presented as escaped Unicode codes in UTF-8.
* Fixed issue with date time format in /ping response.
* Open API specification updated on [GitHub](https://github.com/regulaforensics/DocumentReader-web-openapi).
* Clients and packages updated.

## v1.2

#### Fixed

* Issue with &lt;clear/&gt; and &lt;clear&gt;&lt;clear&gt; and tag in the config file

#### Changed

* Response codes for transaction status and results
  * if there's no result and there was no error during processing, the response will be marked as successful \(HTTP OK 200\) and the payload will contain null
  * if there's no result, and there was an error during processing, the response will be marked as unsuccessful \(HTTP Server Error 500\) and the payload will contain an error message
  * transaction status will be marked as unsuccessful and contain an error message if there was an error

#### Added

* optional configuration parameter &lt;SdkMaxProcessingTime&gt;, which allows to override 10 second transaction processing timeout

