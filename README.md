# zabbix-cloudwatch
Cloudwatch integration for Zabbix 4.x

## Prerequesites:

* Docker hosted Zabbix 4.x
* Boto3
* Pip3
* Python 3.6.x

Download pip3 sudo apt-get install python3-pip

### Required Pip3 packages

* https://pypi.org/project/configparser/
* https://pypi.org/project/importlib2/
* 


### Guide

1. Create specialized user account(s) in AWS and grant it permissions for required services and API calls (for example `describe_instances()` for EC2)
2. Clone github repo: https://github.com/Nufan1121/zabbix-cloudwatch.git
3. Copy contents of `zabbix-scripts` into Zabbix accessible `/usr/lib/zabbix` directory, change owner of the dir and its contents to the user under which you run Zabbix.
4. [Install](http://boto3.readthedocs.io/en/latest/guide/quickstart.html) system-wide `boto3` package
5. Import `cloudwatch_template.xml` into Zabbix
6. Put credentials of AWS account(s) created into `/usr/lib/zabbix/scripts/conf/aws.conf` as formatted as below (supports multiple accounts)
```
[utrack]
key={{ AWS KEY }}
secret={{ AWS SECRET }}
```
7. Create host within Zabbix specifying 0.0.0.0 as the host interface IP and link the previously imported template. Change macro values `ACCOUNT` and `REGION` to correspond to your AWS accounts: 
8. Enable/Disable all discovery rules/items/triggers you think necessary, add new or modify existing ones.

Default template has rules and items for following services:
* EC2 (requires `describe_instances()` API call permissions)
* RDS (`describe_db_instances()` API call)
* ELB (`describe_load_balancers()` API call)
* EMR (`list_clusters()` API call)
* ELBv2 (`describe_target_groups()` API call)
* S3 (`list_buckets()` API call)

Originally created by: twitter [@wawastein](https://twitter.com/wawastein).
