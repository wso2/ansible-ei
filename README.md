# WSO2 Enterprise Integrator Ansible scripts

This repository contains the Ansible scripts for installing and configuring WSO2 Enterprise Integrator.

## Supported Operating Systems
- Ubuntu 16.04 or higher
- CentOS 7

## Supported Ansible Versions

- Ansible 2.6.2

## Directory Structure
```

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
