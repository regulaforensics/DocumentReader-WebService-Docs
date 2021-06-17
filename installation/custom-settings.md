# Settings

### **Logging**

There are **3** log types in our service: 
1. access logs - are just standard **HTTP** access logs.
2. application logs  - regular application logs, including errors and debug messages.
3. document process results logs - stores document processing **input** and **results** in JSON format. 
   **Space-consuming** option, up to a few tens of Mb per request. **Disabled** by default.

| Option          | Default              | Description         |
| --------------- | -------------------- | ------------------- |
| **DOCREADER_LOGS_ACCESS_CONSOLE** | "false"  | Controls whether to print access logs to a console.  |
| **DOCREADER_LOGS_ACCESS_FILE**    | "false"  | Controls whether to save access logs to a file.  |
| **DOCREADER_LOGS_ACCESS_FILE_PATH**  | "logs/access/document-reader-access.log"  | Specifies a file to save access logs if **DOCREADER_LOGS_ACCESS_FILE** enabled.  |
| | | |
| **DOCREADER_LOGS_APP_CONSOLE** | "true"  | Controls whether to print application logs to a console. |
| **DOCREADER_LOGS_APP_FILE** | "false" on Docker **\/** "true" on other installations  | Controls whether to save application logs to a file.  |
| **DOCREADER_LOGS_APP_FILE_PATH**    | "logs/app/document-reader-app.log"  | Specifies a file to save access logs if **DOCREADER_LOGS_APP_FILE** enabled.  
| | | |
| **DOCREADER_PROCESS_RESULTS_LOG_PATH** | "logs/process"  | Specifies a folder to save document process results. Final output is a **zip** file, located in **yyyy/mm/dd/hh** folder under specified in this property root path.  |
| | | |
| **DOCREADER_LOGS_FORMATTER** | "text"  | Possible values: **"text"** / **"json"**. Some log collectors require logs to be printed in json format.  |

Access and applications logs are printed to **stdout**.
For access and applications logs files **day-based** rotation occurs every **midnight UTC**. 
Service **keeps** the last **30 days** of logs files.

### General

* **DOCREADER\_BIND**: the bind ip\_address:port, default **0.0.0.0:8080**
* **DOCREADER\_BACKLOG**: the maximum number of requests in a queue, default **20**
* **DOCREADER\_WORKERS**: the number of workers to process requests, default **1**
* **DOCREADER\_LIC\_URL**: the URL to regula.license file for further download, if the mount option is not available, default **None** \(low priority over mounted file\)
* **DOCREADER\_ENABLE\_DEMO\_WEB\_APP**: enable demo site, default **true**

#### HTTPS

* **DOCREADER\_CERT\_FILE**: the absolute path to SSL certificate file
* **DOCREADER\_KEY\_FILE**: the absolute path to SSL key file

#### CORS

* **DOCREADER\_CORS\_ORIGINS**: allowed cors origins, default **same-origin policy**
* **DOCREADER\_CORS\_METHODS**: allowed cors methods, default **all methods**
* **DOCREADER\_CORS\_HEADERS**: allowed cors headers, default **all headers**



**NOTE** Custom options can be overridden on the container start:

```text
docker run -p host_port:8080 -v host_path_to_license_folder/regula.license:/app/extBin/unix_x64/regula.license -e DOCREADER_WORKERS=4 regulaforensics/docreader:tagname
```

### Enable HTTPS mode

#### Option 1. Recommended. Nginx as a reverse-proxy

Run Nginx as a frontend container for HTTPS processing and proxy service requests to the backend docreader container. [link](https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/)

#### Option 2. Docreader via HTTPS

To run the docreader service via https:

* add 644 permissions to certificates so the server is able to read certificates
* pass cert.crt & cert.key files to the container
* pass DOCREADER\_CERT\_FILE, DOCREADER\_KEY\_FILE environment variables
* forward container port to 8443 host port

```text
chmod 644 ~/cert.crt ~/cert.key
docker run -it -p 8443:8080 -v ~/regula.license:/app/extBin/unix_x64/regula.license -v ~/cert.crt:/app/cert.crt -v ~/cert.key:/app/cert.key -e DOCREADER_CERT_FILE="/app/cert.crt" -e DOCREADER_KEY_FILE="/app/cert.key" regulaforensics/docreader
```

### 

