# Docker

#### Windows 10:

1. Install Docker Desktop using the following instruction basing on your Windows edition:

* [Installing Docker Desktop on Windows 10 Pro, Enterprise, and Education](https://docs.docker.com/docker-for-windows/install/) \(_clickable_\)
* [Installing Docker Desktop on Windows 10 Home](https://docs.docker.com/docker-for-windows/install-windows-home/) \(_clickable_\)

1. Start Docker Desktop application
2. Put your license to your Desktop directory
3. Open the Command line and execute the following command:

**Hint** To open Command line: press _WIN_ button, type _cmd_ and press _Enter_

```text
docker run -d -p 8080:8080 -v C:\%HOMEPATH%\Desktop\regula.license:/app/extBin/unix_x64/regula.license regulaforensics/docreader:latest
```

1. Enter the following address in a web browser: [http://localhost:8080/](http://localhost:8080/) to verify service is up and running

#### Linux/macOS:

1. Install Docker Engine:

* [Linux platforms](https://docs.docker.com/engine/install/#server) \(_clickable_\)
* [Installing Docker Desktop on Mac](https://docs.docker.com/docker-for-mac/install/) \(_clickable_\)

1. Put your license to your user's home \(/home/username/\) directory
2. Open a terminal and execute:

   ```text
   docker run -p 8080:8080 -v ~/regula.license:/app/extBin/unix_x64/regula.license regulaforensics/docreader:latest
   ```

3. Enter the following address in a web browser: [http://localhost:8080/](http://localhost:8080/) to verify service is up and running



All required information regarding deploying containerized Document Reader Web API can be found on our official Docker Hub repository page.

[Docker Hub](https://hub.docker.com/r/regulaforensics/docreader) \(clickable\)

