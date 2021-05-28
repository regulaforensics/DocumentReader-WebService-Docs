# Changelog

## April 5, 2021 - v5.5

* Added **CERT\_FILE** and **KEY\_FILE** environment variables specifying path for an external SSL certificate and private key for enabling HTTPS.
* Added pass-back object: if included in the request as _**passBackObject**_ JSON object will be returned in response the same way.
* Fixed issue with missing write to folder permissions for request logging on start-up.
* Fixed issue with translating old-style API request capabilities value into scenario value.
* Fixed issue with non-ASCII characters presented as escaped Unicode codes in UTF-8.
* Fixed issue with date time format in /ping response.



