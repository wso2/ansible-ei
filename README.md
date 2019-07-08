# WSO2 Enterprise Integrator Ansible scripts

This repository contains the Ansible scripts for installing and configuring WSO2 Enterprise Integrator.

## Supported Operating Systems
- Ubuntu 16.04 or higher
- CentOS 7

## Supported Ansible Versions

- Ansible 2.8.0

## Directory Structure
```
.
├── dev
│   ├── group_vars
│   │   └── ei.yml
│   ├── host_vars
│   │   ├── analytics_dashboard_1.yml
│   │   ├── analytics_worker_1.yml
│   │   ├── bps_1.yml
│   │   ├── broker_1.yml
│   │   ├── integrator_1.yml
│   │   └── msf4j_1.yml
│   └── inventory
├── docs
│   └── images
├── files
│   ├── lib
│   │   ├── amazon-corretto-8.202.08.2-linux-x64.tar.gz
│   │   └── mysql-connector-java-5.1.47-bin.jar
│   └── packs
│       └── wso2ei-6.5.0.zip
├── issue_template.md
├── LICENSE
├── pull_request_template.md
├── README.md
├── roles
│   ├── analytics-dashboard
│   │   ├── tasks
│   │   │   ├── custom.yml
│   │   │   └── main.yml
│   │   └── templates
│   │       ├── carbon-home
│   │       │   ├── bin
│   │       │   │   └── analytics-dashboard.sh.j2
│   │       │   └── wso2
│   │       │       └── analytics
│   │       │           └── conf
│   │       │               └── dashboard
│   │       │                   └── deployment.yaml
│   │       └── wso2ei-analytics-dashboard.service.j2
│   ├── analytics-worker
│   │   ├── tasks
│   │   │   ├── custom.yml
│   │   │   └── main.yml
│   │   └── templates
│   │       ├── carbon-home
│   │       │   ├── bin
│   │       │   │   └── analytics-worker.sh.j2
│   │       │   └── wso2
│   │       │       └── analytics
│   │       │           └── conf
│   │       │               └── worker
│   │       │                   └── deployment.yaml
│   │       └── wso2ei-analytics-worker.service.j2
│   ├── bps
│   │   ├── tasks
│   │   │   ├── custom.yml
│   │   │   └── main.yml
│   │   └── templates
│   │       ├── carbon-home
│   │       │   └── wso2
│   │       │       └── business-process
│   │       │           ├── bin
│   │       │           │   └── wso2server.sh
│   │       │           └── conf
│   │       │               ├── axis2
│   │       │               │   └── axis2.xml.j2
│   │       │               ├── carbon.xml.j2
│   │       │               ├── datasources
│   │       │               │   ├── activiti-datasources.xml.j2
│   │       │               │   ├── bps-datasources.xml.j2
│   │       │               │   └── master-datasources.xml.j2
│   │       │               ├── registry.xml.j2
│   │       │               └── user-mgt.xml.j2
│   │       └── wso2ei-bps.service.j2
│   ├── broker
│   │   ├── tasks
│   │   │   ├── custom.yml
│   │   │   └── main.yml
│   │   └── templates
│   │       ├── carbon-home
│   │       │   └── wso2
│   │       │       └── broker
│   │       │           ├── bin
│   │       │           │   └── wso2server.sh
│   │       │           └── conf
│   │       │               ├── axis2
│   │       │               │   └── axis2.xml.j2
│   │       │               ├── carbon.xml.j2
│   │       │               ├── datasources
│   │       │               │   └── master-datasources.xml.j2
│   │       │               ├── registry.xml.j2
│   │       │               └── user-mgt.xml.j2
│   │       └── wso2ei-broker.service.j2
│   ├── common
│   │   └── tasks
│   │       ├── custom.yml
│   │       └── main.yml
│   └── integrator
│       ├── tasks
│       │   ├── custom.yml
│       │   └── main.yml
│       └── templates
│           ├── carbon-home
│           │   ├── bin
│           │   │   └── integrator.sh.j2
│           │   ├── conf
│           │   │   ├── axis2
│           │   │   │   └── axis2.xml.j2
│           │   │   ├── carbon.xml.j2
│           │   │   ├── datasources
│           │   │   │   └── master-datasources.xml.j2
│           │   │   ├── jndi.properties.j2
│           │   │   ├── registry.xml.j2
│           │   │   ├── synapse.properties.j2
│           │   │   ├── tomcat
│           │   │   │   └── catalina-server.xml.j2
│           │   │   └── user-mgt.xml.j2
│           │   └── repository
│           │       └── deployment
│           │           └── server
│           │               └── eventpublishers
│           │                   ├── MessageFlowConfigurationPublisher.xml.j2
│           │                   └── MessageFlowStatisticsPublisher.xml.j2
│           └── wso2ei-integrator.service.j2
├── scripts
│   ├── update.sh
│   └── update_README.md
└── site.yml
```

Packs could be either copied to a local directory, or downloaded from a remote location.

## Packs to be Copied

Copy the following files to `files/packs` directory.

1. [WSO2 Enterprise Integrator 6.5.0 package](https://wso2.com/integration/install/)

Copy the following files to `files/lib` directory.

1. [MySQL Connector/J](https://dev.mysql.com/downloads/connector/j/5.1.html)
2. [Amazon Coretto for Linux x64 JDK](https://docs.aws.amazon.com/corretto/latest/corretto-8-ug/downloads-list.html)

## Downloading from remote location

In **group_vars**, change the values of the following variables in all groups:
1. The value of `pack_location` should be changed from "local" to "remote"
2. The value of `remote_jdk` should be changed to the URL in which the JDK should be downloaded from, and remove it as a comment.
3. The value of `remote_pack` should be changed to the URL in which the package should be downloaded from, and remove it as a comment.

## Running WSO2 Enterprise Integrator Ansible scripts

### 1. Run the existing scripts without customization
The existing Ansible scripts contain the configurations to set-up WSO2 Enterprise Integrator. In order to deploy that, you need to replace the `[ip_address]` and `[ssh_user]` given in the `inventory` file under `dev` folder by the IP of the location where you need to host the Enterprise Integrator and the SSH user. An example is given below.
```
[ei]
wso2ei ansible_host=172.28.128.4 ansible_user=vagrant
```

Run the following command to run the scripts.

`ansible-playbook -i dev site.yml`

If you need to alter the configurations given, please change the parameterized values in the yaml files under `group_vars` and `host_vars`.

### 2. Customize the WSO2 Ansible scripts

The templates that are used by the Ansible scripts are in j2 format in-order to enable parameterization.

#### Step 1
Uncomment the following line in `main.yml` under the role you want to customize.
```
- import_tasks: custom.yml
```

#### Step 2
Add the configurations to the `custom.yml`. A sample is given below.

```
- name: "Copy custom file"
  template:
    src: path/to/example/file/example.xml.j2
    dest: destination/example.xml.j2
  when: "(inventory_hostname in groups['sp'])"
```

Follow the steps mentioned under `docs` directory to customize/create new Ansible scripts and deploy the recommended patterns.

## Performance Tuning

System configurations can be changed through Ansible to optimize OS level performance. Performance tuning can be enabled by changing `enable_performance_tuning` in `dev/group_vars/ei.yml` to `true`.

System files that will be updated when performance tuning are enabled is available in `files/system`. Update the configuration values according to the requirements of your deployment.
