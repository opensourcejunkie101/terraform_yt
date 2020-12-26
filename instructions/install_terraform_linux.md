## HOW TO INSTALL TERRAFORM ON LINUX OS

### 1. Download `unzip` and `wget`

Terraform is packaged under zip by Hashicorp, hence unzip is required to extract the terraform binary and execute it. `wget` will be used for downloading the files from remote sources.

* RHEL and CentOS
```
sudo yum install wget unzip -y
```

* Ubuntu and Debian
```
sudo apt install wget unzip -y
```

### 2. Download the terraform binaries

Terraform binaries are maintained and managed by Hashicorp at this location - https://releases.hashicorp.com/terraform/

```
mkdir ~/Terraform && ~/Terraform

TERRAFORM_VERSION="0.12.29"

wget https://releases.hashicorp.com/terraform/0.12.29/terraform_${TERRAFORM_VERSION}_linux_amd64.zip -O terraform_${TERRAFORM_VERSION}.zip

```

### 3. Extract and Add binaries to the `PATH`

Unzip the terraform binary
```
unzip terraform_${TERRAFORM_VERSION}.zip
```

Add the binaries to PATH variable
```
# to list all environment path variables
echo $PATH

sudo mv terraform /usr/local/bin/
```

### 4. Validate terraform Installation
```
terraform version
```

