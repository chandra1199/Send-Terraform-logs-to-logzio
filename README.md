# Send-Terraform-logs-to-logzio

# Terraform-logs-to-logzio

# Install td-agent-bit in ubuntu 20.04
```
# Install td-agent-bit in ubuntu 20.04
wget -qO - https://packages.fluentbit.io/fluentbit.key | sudo apt-key add -
open /etc/apt/sources.list file and add below line at the bootom of the file
deb https://packages.fluentbit.io/ubuntu/focal focal main
sudo apt-get update
sudo apt-get install td-agent-bit
sudo service td-agent-bit start
sudo service td-agent-bit status
```
# Install and configure the Logz.io plugin
```
wget -O /etc/td-agent-bit/out_logzio.so \
https://github.com/logzio/fluent-bit-logzio-output/raw/master/build/out_logzio-linux.so
```
# Open td-agent-bit.conf file(/etc/td-agent-bit/td-agent-bit.conf and put following content
```
[SERVICE]
    flush 5
    daemon Off
    log_level info
    parsers_file parsers.conf
    plugins_file plugins.conf
    http_server Off
    http_listen 0.0.0.0

[INPUT]
    Name tail
    Path /tmp/tf.log

[OUTPUT]
    Name  logzio
    Match *
    logzio_token here mention your logzio account token
    logzio_url   https://listener.logz.io:8071
```
# Place below content in plugins.conf file(/etc/td-agent-bit/plugins.conf)

```
[PLUGINS]
    # Path /path/to/out_gstdout.so
    Path /etc/td-agent-bit/out_logzio.so
```
# Restart td-agent-bit
```
sudo service td-agent-bit restart
```
# Check td-agent-bit-status
```
sudo service td-agent-bit status
```
# Install terraform on ubuntu 20.04
```
wget https://releases.hashicorp.com/terraform/1.1.2/terraform_1.1.2_linux_amd64.zip
sudo apt install zip -y
sudo unzip terraform_1.1.2_linux_amd64.zip
sudo mv terraform /usr/local/bin/
terraform version
```
# configure aws credentials
```
aws configure --profile example-user
```
# Export TF_LOG, TF_LOG_PATH and AWS_PROFILE variables
```
export TF_LOG_PATH=/tmp/tf.log
export TF_LOG=DEBUG
export AWS_PROFILE=give your profile name
```
# clone git repo
```
git -T git@gitlab.com[ To check whether you are able to access gitlab repo]
git clone "repo url"
cd repo name
execute terraform commands in tf files location
```


    
