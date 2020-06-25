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

cd $GOPATH/src/github.com/alibaba/terraform-provider
export ALICLOUD_ACCESS_KEY=xxx
export ALICLOUD_SECRET_KEY=xxx
export ALICLOUD_REGION=xxx
export ALICLOUD_ACCOUNT_ID=xxx
export outfile=gotest.out
TF_ACC=1 TF_LOG=INFO go test ./alicloud -v -run=TestAccAlicloud -timeout=1440m | tee $outfile
go2xunit -input $outfile -output $GOPATH/tests.xml
-> Note: The last line is optional, it allows to convert test results into a XML format compatible with xUnit.

Because some features are not available in all regions, the following environment variables can be set in order to skip tests that use these features:

ALICLOUD_SKIP_TESTS_FOR_SLB_SPECIFICATION=true - Server Load Balancer with guaranteed performance specifications (old implementation has only shared performance)
ALICLOUD_SKIP_TESTS_FOR_SLB_PAY_BY_BANDWIDTH=true - Server Load Balancer with a "pay by bandwidth" billing method (mostly available in China)
ALICLOUD_SKIP_TESTS_FOR_FUNCTION_COMPUTE=true - Function Compute
ALICLOUD_SKIP_TESTS_FOR_PVTZ_ZONE=true - Private Zone
ALICLOUD_SKIP_TESTS_FOR_RDS_MULTIAZ=true - Apsara RDS with multiple availability zones
ALICLOUD_SKIP_TESTS_FOR_CLASSIC_NETWORK=true - Classic network configuration
Common problems
Error configuring: 1 error(s) occurred:
* Incompatible API version with plugin. Plugin version: 2, Ours: 1

# fix by manually setting the branch in the sources
cd src/github.com/hashicorp/terraform/
git checkout v<YOUR_TF_VERSION_HERE>
cd -

# rebuild
sudo -E "PATH=$PATH" make all
