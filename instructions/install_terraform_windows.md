## HOW TO INSTALL TERRAFORM ON WIDNOW WITH POWERSHELL


### 1. Download the terraform binaries

Terraform binaries are maintained and managed by Hashicorp at this location - https://releases.hashicorp.com/terraform/

```
$TARGET_DIR = 'C:\Terraform\' 
$TERRAFORM_VERSION = '0.12.29'
$TERRAFORM_URI = 'https://releases.hashicorp.com/terraform/' + $TERRAFORM_VERSION + '/terraform_' + $TERRAFORM_VERSION + '_windows_amd64.zip'
$TERRAFORM_ZIP = $TARGET_DIR + 'terraform_' + $TERRAFORM_VERSION + '.zip'

Invoke-WebRequest -Uri $TERRAFORM_URI -OutFile ( New-Item -Path $TERRAFORM_ZIP  -Force )

```

### 2. Extract and Add binaries to the `PATH`

Unzip the terraform binary
```
Expand-Archive $TERRAFORM_ZIP -DestinationPath ( New-Item -Path $TARGET_DIR\bin\ -ItemType "directory" -Force )

```

Add the binaries to PATH variable (ensure powershell is opened with Admin rights)
```
# to list all environment path variables
Write-Host $env:Path

$env:Path += ";$TARGET_DIR\bin"
```

Remove the terraform zip
```
Remove-Item $TARGET_DIR\*.zip
```

### 3. Validate terraform Installation
```
terraform version
```

Note: To add terraform binary path permanantly - [Windows Environment Variables](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_environment_variables?view=powershell-7.1#using-and-changing-environment-variables)
