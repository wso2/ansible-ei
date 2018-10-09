# WSO2 Enterprise Integrator Ansible scripts

This repository contains the Ansible scripts for installing and configuring WSO2 Enterprise Integrator.

## Supported Operating Systems
- Ubuntu 16.04 or higher
- CentOS 7

## Supported Ansible Versions

- Ansible 2.6.2

## Directory Structure
```
.
├── dev
│   ├── group_vars
│   │   └── ei.yml
│   ├── host_vars
│   │   ├── analytics_1.yml
│   │   ├── bps_1.yml
│   │   ├── broker_1.yml
│   │   ├── integrator_1.yml
│   │   ├── micro_integrator_1.yml
│   │   └── msf4j_1.yml
│   └── inventory
├── docs
│   └── images
├── files
│   ├── mysql-connector-java-5.1.45-bin.jar
│   ├── wso2ei-linux-installer-x64-6.3.0.deb
│   └── wso2ei-linux-installer-x64-6.3.0.rpm
├── issue_template.md
├── LICENSE
├── pull_request_template.md
├── README.md
├── roles
│   ├── analytics
│   │   ├── tasks
│   │   │   ├── custom.yml
│   │   │   └── main.yml
│   │   └── templates
│   │       ├── carbon-home
│   │       │   ├── bin
│   │       │   │   └── analytics.sh.j2
│   │       │   └── wso2
│   │       │       └── analytics
│   │       │           ├── bin
│   │       │           │   └── wso2server.sh
│   │       │           └── conf
│   │       │               ├── carbon.xml
│   │       │               ├── datasources
│   │       │               │   ├── analytics-datasources.xml
│   │       │               │   └── master-datasources.xml
│   │       │               ├── registry.xml
│   │       │               └── user-mgt.xml
│   │       └── wso2ei-analytics.service.j2
│   ├── bps
│   │   ├── tasks
│   │   │   ├── custom.yml
│   │   │   └── main.yml
│   │   └── templates
│   │       ├── carbon-home
│   │       │   ├── bin
│   │       │   │   └── business-process.sh.j2
│   │       │   └── wso2
│   │       │       └── business-process
│   │       │           └── conf
│   │       │               ├── bps.xml
│   │       │               ├── carbon.xml
│   │       │               ├── datasources
│   │       │               │   ├── activiti-datasources.xml
│   │       │               │   ├── bps-datasources.xml
│   │       │               │   └── master-datasources.xml
│   │       │               ├── registry.xml
│   │       │               └── user-mgt.xml
│   │       └── wso2ei-bps.service.j2
│   ├── broker
│   │   ├── tasks
│   │   │   ├── custom.yml
│   │   │   └── main.yml
│   │   └── templates
│   │       ├── carbon-home
│   │       │   ├── bin
│   │       │   │   └── broker.sh.j2
│   │       │   └── wso2
│   │       │       └── broker
│   │       │           └── conf
│   │       │               ├── broker.xml
│   │       │               ├── carbon.xml
│   │       │               ├── datasources
│   │       │               │   └── master-datasources.xml
│   │       │               ├── registry.xml
│   │       │               └── user-mgt.xml
│   │       └── wso2sp-editor.service.j2
│   ├── common
│   │   └── tasks
│   │       ├── custom.yml
│   │       └── main.yml
│   ├── integrator
│   │   ├── tasks
│   │   │   ├── custom.yml
│   │   │   └── main.yml
│   │   └── templates
│   │       ├── carbon-home
│   │       │   ├── bin
│   │       │   │   └── integrator.sh.j2
│   │       │   ├── conf
│   │       │   │   ├── axis2
│   │       │   │   │   └── axis2.xml
│   │       │   │   ├── carbon.xml
│   │       │   │   ├── datasources
│   │       │   │   │   └── master-datasources.xml
│   │       │   │   ├── jndi.properties
│   │       │   │   ├── registry.xml
│   │       │   │   ├── synapse.properties
│   │       │   │   ├── tomcat
│   │       │   │   │   └── catalina-server.xml
│   │       │   │   └── user-mgt.xml
│   │       │   └── repository
│   │       │       └── deployment
│   │       │           └── server
│   │       │               └── eventpublishers
│   │       │                   ├── MessageFlowConfigurationPublisher.xml
│   │       │                   └── MessageFlowStatisticsPublisher.xml
│   │       └── wso2ei-integrator.service.j2
│   ├── micro_integrator
│   │   ├── tasks
│   │   │   ├── custom.yml
│   │   │   └── main.yml
│   │   └── templates
│   │       ├── carbon-home
│   │       │   ├── bin
│   │       │   │   └── micro-integrator.sh.j2
│   │       │   └── wso2
│   │       │       └── micro-integrator
│   │       │           ├── conf
│   │       │           │   ├── axis2
│   │       │           │   │   └── axis2.xml
│   │       │           │   ├── carbon.xml
│   │       │           │   ├── datasources
│   │       │           │   │   └── master-datasources.xml
│   │       │           │   ├── jndi.properties
│   │       │           │   └── tomcat
│   │       │           │       └── catalina-server.xml
│   │       │           └── repository
│   │       │               └── deployment
│   │       │                   └── server
│   │       │                       └── eventpublishers
│   │       │                           ├── MessageFlowConfigurationPublisher.xml
│   │       │                           └── MessageFlowStatisticsPublisher.xml
│   │       └── wso2ei-micro-integrator.service.j2
│   └── msf4j
│       ├── tasks
│       │   ├── custom.yml
│       │   └── main.yml
│       └── templates
│           ├── carbon-home
│           │   ├── bin
│           │   │   └── msf4j.sh.j2
│           │   └── wso2
│           │       └── msf4j
│           │           └── conf
│           │               ├── carbon.yml
│           │               ├── data-bridge
│           │               │   ├── client-truststore.jks
│           │               │   └── data-agent-config.xml
│           │               └── datasources
│           │                   └── metrics-datasources.xml
│           └── wso2ei-msf4j.service.j2
└── site.yml
```

## Packs to be Copied

Copy the following files to `files` directory.

1. [WSO2 Enterprise Integrator 6.3.0 package](https://wso2.com/integration/install/)
2. [MySQL Connector/J](https://dev.mysql.com/downloads/connector/j/5.1.html)

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
