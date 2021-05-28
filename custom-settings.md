# Custom settings

## **Logging Settings**

There are 3 log types in our service: access logs, app logs, and process logs.

**Access logs** _-_ are just standard HTTP access logs.

```text
DOCREADER_LOGS_ACCESS_CONSOLE="false"
DOCREADER_LOGS_ACCESS_FILE="false"
DOCREADER_LOGS_ACCESS_FILE_PATH='logs/access/document-reader-access.log'
```

**App logs** _-_ all other application logs. Error logs are printed under the **error** log level.

```text
DOCREADER_LOGS_APP_CONSOLE="true"
DOCREADER_LOGS_APP_FILE="true"
DOCREADER_LOGS_APP_FILE_PATH='logs/app/document-reader-app.log'
```

**Process logs** _-_ store document processing input and results in JSON format. Space-consuming option, up to a few tens of Mb per request. Disabled by default.

```text
DOCREADER_PROCESS_RESULTS_LOG_PATH="logs/process"
```

**Logs format**

```text
DOCREADER_LOGS_FORMATTER="text"
# or DOCREADER_LOGS_FORMATTER="json"
```

The service writes console logs to stdout. Day-based file rotation occurs every midnight UTC. Service keeps the last 30 days of file logs.

## General

* **DOCREADER\_BIND**: the bind ip\_address:port, default **0.0.0.0:8080**
* **DOCREADER\_BACKLOG**: the maximum number of requests in a queue, default **20**
* **DOCREADER\_WORKERS**: the number of workers to process requests, default **1**
* **DOCREADER\_LIC\_URL**: the URL to regula.license file for further download, if the mount option is not available, default **None** \(low priority over mounted file\)
* **DOCREADER\_ENABLE\_DEMO\_WEB\_APP**: enable demo site, default **true**

### HTTPS

* **DOCREADER\_CERT\_FILE**: the absolute path to SSL certificate file
* **DOCREADER\_KEY\_FILE**: the absolute path to SSL key file

### CORS

* **DOCREADER\_CORS\_ORIGINS**: allowed cors origins, default **same-origin policy**
* **DOCREADER\_CORS\_METHODS**: allowed cors methods, default **all methods**
* **DOCREADER\_CORS\_HEADERS**: allowed cors headers, default **all headers**

**NOTE** Custom options can be overridden on the container start:

```text
docker run -p host_port:8080 -v host_path_to_license_folder/regula.license:/app/extBin/unix_x64/regula.license -e DOCREADER_WORKERS=4 regulaforensics/docreader:tagname
```

## Enable HTTPS mode

### Option 1. Recommended. Nginx as a reverse-proxy

Run Nginx as a frontend container for HTTPS processing and proxy service requests to the backend docreader container. [link](https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/)

### Option 2. Docreader via HTTPS

To run the docreader service via https:

* add 644 permissions to certificates so the server is able to read certificates
* pass cert.crt & cert.key files to the container
* pass DOCREADER\_CERT\_FILE, DOCREADER\_KEY\_FILE environment variables
* forward container port to 8443 host port

```text
chmod 644 ~/cert.crt ~/cert.key
docker run -it -p 8443:8080 -v ~/regula.license:/app/extBin/unix_x64/regula.license -v ~/cert.crt:/app/cert.crt -v ~/cert.key:/app/cert.key -e DOCREADER_CERT_FILE="/app/cert.crt" -e DOCREADER_KEY_FILE="/app/cert.key" regulaforensics/docreader
```

