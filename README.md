# airflow-rpm

Build scripts for generating Apache Airflow RPM files.
Tested on CentOS 7

## Install Build Requirements
```
$> sudo yum install epel-release
$> sudo yum update
$> sudo yum install rpm-build mariadb-devel libffi-devel cyrus-sasl-devel gcc-c++
$> sudo yum install python36 python36-devel python36-libs python36-numpy python36-pbr python36-setuptools python36-pip
$> sudo yum install python36-pysocks python36-root python36-six python36-test python36-urllib3
```
># not need $> sudo pip install setuptools --upgrade
># not need $> sudo pip install pip --upgrade

## Clone 
```
$> git clone https://github.com/naototty/airflow-rpm.git
$> cd airflow-rpm
```

## Configure Version + Packages
Configure Apache Airflow version on pip
(Apache Airflow on https://pypi.org/project/apache-airflow/; start version >= 1.8.1)
```
$> cat Makefile
...
version = 1.8.1
```

## Configure Airflow Packages as needed
```
$> cat Makefile
...
## packages = devel,devel_hadoop,celery,crypto,jdbc,hdfs,kerberos,ldap,mysql,password,postgres,rabbitmq
packages = devel,celery,crypto,password,postgres,s3
```

## Build RPM
```
$> make
```

## Install RPM
```
$> sudo yum install rpmbuild/RPMS/x86_64/airflow-1.7.1.3-1.el7.centos.x86_64.rpm
```

## Airflow Init Server Configuration
```
$> sudo su airflow
$> AIRFLOW_HOME=/usr/share/airflow \
AIRFLOW_CONFIG=${AIRFLOW_HOME}/airflow.cfg \
airflow version
$> cat /usr/share/airflow/airflow.cfg
```

## Airflow InitDB
```
$> AIRFLOW_HOME=/usr/share/airflow \
AIRFLOW_CONFIG=${AIRFLOW_HOME}/airflow.cfg \
airflow initdb
$> exit
```

## Airflow Services Start (as needed)
```
$> sudo systemctl start airflow-flower
$> sudo systemctl start airflow-kerberos
$> sudo systemctl start airflow-scheduler
$> sudo systemctl start airflow-webserver
$> sudo systemctl start airflow-worker
```

## Airflow Service Status
```
$> sudo systemctl status airflow-flower
$> sudo systemctl status airflow-kerberos
$> sudo systemctl status airflow-scheduler
$> sudo systemctl status airflow-webserver
$> sudo systemctl status airflow-worker
```

## Airflow Services Start On Boot (as needed)
```
$> sudo systemctl enable airflow-flower
$> sudo systemctl enable airflow-kerberos
$> sudo systemctl enable airflow-scheduler
$> sudo systemctl enable airflow-webserver
$> sudo systemctl enable airflow-worker
```


