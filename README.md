# alibabatf

Read https://www.terraform.io/docs/providers/alicloud/r/instance.html for more info.

Read https://www.terraform.io/docs/providers/alicloud/index.html for more info.

Example
Example modules can be found in the terraform/examples directory.

Developer notes
Setting up
Install Terraform: https://www.terraform.io/intro/getting-started/install.html
Install golang: https://golang.org/doc/install
Install goimports: https://godoc.org/golang.org/x/tools/cmd/goimports
go get golang.org/x/tools/cmd/goimports
Finally:
mkdir -p $GOPATH/src/github.com/alibaba
cd $GOPATH/src/github.com/alibaba
git clone https://github.com/alibaba/terraform-provider.git

# switch to project
cd $GOPATH/src/github.com/alibaba/terraform-provider

# build provider

## Mac
make dev
## Linux
make devlinux
## Windows
make devwin

# install modules
terraform get

# set the creds
export ALICLOUD_ACCESS_KEY="***"
export ALICLOUD_SECRET_KEY="***"
export ALICLOUD_REGION="***"
export ALICLOUD_ACCOUNT_ID="***"

# you're good to start rocking
# alicloud.tf contains the default example
terraform plan
# terraform apply
# terraform destroy
