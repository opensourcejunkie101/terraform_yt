## HOW TO INSTALL TERRAFORM ON WIDNOW WITH POWERSHELL

### 1. Create `unzip` function and validate `wget` on powershell

Terraform is packaged under zip by Hashicorp, hence unzip is required to extract the terraform binary and execute it. `wget` will be used for downloading the files from remote sources.


```
$outputDir = 'C:\Terraform\' 
$TERRAFORM_VERSION = '0.12.29'

Invoke-WebRequest -Uri 'https://releases.hashicorp.com/terraform/0.12.29/terraform_' + $TERRAFORM_VERSION + '_linux_amd64.zip' -OutFile $outputDir 

$ExtractShell = New-Object -ComObject Shell.Application 
$Files = $ExtractShell.Namespace($ZipFile).Items() 
$ExtractShell.NameSpace($Destination).CopyHere($Files) 
Start-Process $Destination

```

* Create unzip function
```
function unzip
{
    param([string]$zipfile, [string]$outpath)

    [System.IO.Compression.ZipFile]::ExtractToDirectory($zipfile, $outpath)
}
```

* Validate wget cmlet
```
Get-Command wget
```

### 2. Download the terraform binaries

Terraform binaries are maintained and managed by Hashicorp at this location - https://releases.hashicorp.com/terraform/

```
mkdir ~/Terraform && cd ~/Terraform

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

