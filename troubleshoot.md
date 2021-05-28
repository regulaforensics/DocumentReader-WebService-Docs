# Troubleshoot

### Supplied license either corrupted or expired

* Check if the regula.license file is in the expected location. The absolute path should be as follows: C:\ProgramData\Regula\Licenses\regula.license.
* Check if the Web API has access to the internet, at least to [**https://lic.regulaforensics.com/**](https://lic.regulaforensics.com/) URL. 
* Check if the license type is "On-line" \(supplied within the OLXXXXX.zip archive\)
* Check if the license is sufficient to request the desired number of workers. Each license is issued for a specific number of workers; thus, it is not possible to run the service if the number of requested workers exceeds the number defined in the license.
* [**Contact us**](https://support.regulaforensics.com/hc/en-us/requests/new) to check whether the license has expired or been deactivated.

### Permanent container restart

* Check if the allocated RAM is sufficient \(at least 2Gb RAM per worker is required\)
* Check if the Web API has access to the internet, at least [**https://lic.regulaforensics.com/**](https://lic.regulaforensics.com/) URL. In case a direct internet connection is not an option, please configure Docker to use the proxy server [**guide**](https://docs.docker.com/network/proxy/).



