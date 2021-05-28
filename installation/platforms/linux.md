# Linux

## Prerequisites

To install Document Reader Web API you need, a 64-bit version of one of these supported OS versions:

**Ubuntu**

* Ubuntu 16.04 \(xenial\)
* Ubuntu 18.04 \(bionic\)
* Ubuntu 20.04 \(focal\)

**Debian**

* Debian 8 \(Jessie\)
* Debian 9 \(Stretch\)
* Debian 10 \(Buster\)

**CentOS**

* CentOS 7
* CentOS 8

{% hint style="info" %}
Document Reader Web API is supported on`x86_64`or`(amd64)`architectures.
{% endhint %}

## Install Document Reader Web API

### Install using the repository

{% tabs %}
{% tab title="Ubuntu" %}
#### Set up the repository

 1. Update the `apt` package index and install packages to allow `apt` using the repository over HTTPS:

```bash
sudo apt-get update
```

```
sudo apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
```

2. Add Regula official GPG key:

```text
curl -fsSL https://downloads.regulaforensics.com/repo/ubuntu/regula.gpg | sudo apt-key add -
```

3.  Use the following command to set up the **stable** repository.

```text
sudo add-apt-repository \
   "deb [arch=amd64] https://downloads.regulaforensics.com/repo/ubuntu \
   $(lsb_release -cs) \
   stable"
```

#### Install Document Reader Web API

 1. Update the `apt` package index and install the _latest version_ of Document Reader Web API, or go to the next step to install a specific version:

```text
sudo apt-get update
```

```text
sudo apt-get install regula-document-reader-webapi
```

2. To install a _specific version_ of Document Reader Web API, list the available versions in the repo, then select and install the required version:

a. List the versions available in your repo:

```text
apt-cache madison regula-document-reader-webapi
```

b. Install a specific version using the version string from the second column

```text
sudo apt-get install regula-document-reader-webapi=<VERSION>
```
{% endtab %}

{% tab title="Debian" %}
#### Set up the repository

 1. Update the `apt` package index and install packages to allow `apt` using the repository over HTTPS:

```bash
sudo apt-get update
```

```
sudo apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
```

2. Add Regula official GPG key:

```text
curl -fsSL https://downloads.regulaforensics.com/repo/debian/regula.gpg | sudo apt-key add -
```

3.  Use the following command to set up the **stable** repository.

```text
sudo add-apt-repository \
   "deb [arch=amd64] https://downloads.regulaforensics.com/repo/debian \
   $(lsb_release -cs) \
   stable"
```

#### Install Document Reader Web API

 1. Update the `apt` package index and install the _latest version_ of Document Reader Web API, or go to the next step to install a specific version:

```text
sudo apt-get update
```

```text
sudo apt-get install regula-document-reader-webapi
```

2. To install a _specific version_ of Document Reader Web API, list the available versions in the repo, then select and install the required version:

a. List the versions available in your repo:

```text
apt-cache madison regula-document-reader-webapi
```

b. Install a specific version using the version string from the second column

```text
sudo apt-get install regula-document-reader-webapi=<VERSION>
```
{% endtab %}

{% tab title="CentOS" %}
#### Set up the repository

Install the `yum-utils` package \(which provides the `yum-config-manager` utility\) and set up the **stable** repository.

```bash
sudo yum install -y yum-utils
```

```
sudo yum-config-manager \
    --add-repo \
    https://downloads.regulaforensics.com/repo/centos/regula.repo
```

#### Install Document Reader Web API

 1. Install the _latest version_ of Document Reader Web API or go to the next step to install a specific version:

```text
sudo yum install regula-document-reader-webapi
```

2. To install a _specific version_ of Document Reader Web API, list the available versions in the repo, then select and install the required version:

a. List the versions available in your repo:

```text
sudo yum list regula-reader --showduplicates | sort -r
```

b. Install a specific version by its fully qualified package name

```text
sudo yum install regula-document-reader-webapi-<VERSION>
```
{% endtab %}
{% endtabs %}

### 

### Install from a package

{% tabs %}
{% tab title="Ubuntu" %}
1. Open [https://downloads.regulaforensics.com/repo/ubuntu/pool/stable/r/regula-document-reader-webapi/](https://downloads.regulaforensics.com/repo/ubuntu/pool/stable/r/regula-document-reader-webapi/), browse the required package dir and download the `.deb` file for the Document Reader Web API version you want to install

   ```text
   wget https://downloads.regulaforensics.com/repo/ubuntu/pool/stable/r/regula-document-reader-webapi/<package>.deb
   ```

2. Install Document Reader Web API

   ```text
   sudo dpkg -i <package>.deb
   ```
{% endtab %}

{% tab title="Debian" %}
1. Open [https://downloads.regulaforensics.com/repo/debian/pool/stable/r/regula-document-reader-webapi/](https://downloads.regulaforensics.com/repo/debian/pool/stable/r/regula-document-reader-webapi/), browse the required package dir and download the `.deb` file for the Document Reader Web API version you want to install

   ```text
   wget https://downloads.regulaforensics.com/repo/debian/pool/stable/r/regula-document-reader-webapi/<package>.deb
   ```

2. Install Document Reader Web API

   ```text
   sudo dpkg -i <package>.deb
   ```
{% endtab %}

{% tab title="CentOS" %}
1. Open [https://downloads.regulaforensics.com/repo/centos/x86\_64/stable/Packages/](https://downloads.regulaforensics.com/repo/centos/x86_64/stable/Packages/) and download the `.rpm` file for the Document Reader Web API version you want to install

   ```text
   wget https://downloads.regulaforensics.com/repo/centos/x86_64/stable/Packages/<package>.rpm
   ```

2. Install Document Reader Web API

   ```text
   sudo rpm -ivh <package>.rpm
   ```
{% endtab %}
{% endtabs %}

## Set up the license

To access all the capabilities of Regula Document Reader Web API, a license is required.

To obtaining the production license or other purchasing information, please [**submit an inquiry**](https://pipedrivewebforms.com/form/49108714c4cf48cd1001d1b8742b84621841159) and our sales team will contact you shortly.

{% hint style="info" %}
Assuming that _regula.license_ file is located at your user's home directory "$HOME/regula.license"
{% endhint %}

1. Copy the obtained _regula.license_ file to the specific folder

```text
sudo cp -ar ~/regula.license /opt/regula/document-reader-webapi/extBin/unix_x64/
```

2. Restart Document Reader Web API service

```text
sudo systemctl restart regula-document-reader-webapi.service
```

