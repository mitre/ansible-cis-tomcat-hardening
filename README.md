# Ansible role `tomcat`

An Ansible role for setting up and hardening Tomcat on RHEL/CentOS 7 or Fedora. Specifically, the responsibilities of this role are to:

- Install packages from the EPEL repository (EL7: Tomcat 7, Fedora 23: Tomcat 8)
- Manage configuration
- Harden Tomcat install

The firewall configuration is not a concern of this role. Use another role for that (e.g. [bertvv.rh-base](https://galaxy.ansible.com/bertvv/rh-base))

## Versioning and State of Development
This project uses the [Semantic Versioning Policy](https://semver.org/). 

### Branches
The master branch contains the latest version of the software leading up to a new release. 

Other branches contain feature-specific updates. 

### Tags
Tags indicate official releases of the project.

Please note 0.x releases are works in progress (WIP) and may change at any time.   

## How to run

1. `bundle install`
2. Set your kitchen environment variable to `.kitchen.docker.yml` or `.kitchen.vagrant.yml` based on preference
  - Example: `export KITCHEN_YAML=.kitchen.vagrant.yml`
3. Run `kitchen converge tomcat`
4. Navigate to http://127.0.0.1:4568
5. Cleanup after with `kitchen destroy tomcat`

## Requirements

No specific requirements

## Role Variables


| Variable                      | Required | Default     | Comments                                                           |
| :---                          | :---     | :---        | :---                                                               |
| `tomcat_port`                 | no       | 8080        | The port number for the Tomcat service (> 1024)                    |
| `tomcat_libraries`            | no       | []          | List of libraries (.jar files) to install in Tomcat lib/ directory |
| `tomcat_deploy_wars`          | no       | []          | List of application archives (.war files) to be deployed           |
| `tomcat_install_admin_webapp` | no       | false       | When true, the admin web application is installed                  |
| `tomcat_roles`                | no       | (see below) | List of user roles to be defined in tomcat-users.xml (see below)   |
| `tomcat_users`                | no       | []          | List of users to be defined in tomcat-users.xml (see below)        |

### Users and roles

When installing the Manager web application, you also need to define at least one user and some roles. See the [Tomcat Documentation](https://tomcat.apache.org/tomcat-7.0-doc/manager-howto.html#Configuring_Manager_Application_Access) for details. The following roles are available by default:

```Yaml
tomcat_roles:
  - manager-gui
  - manager-status
  - manager-script
  - manager-jmx
```

You can override these by redefining `tomcat_roles` in your `host_vars` or `group_vars`.

To enable access to the Manager web application, you must create a username/password and associate one of the `manager-xxx` roles with it. The `tomcat_users` variable takes care of this, e.g.:

```Yaml
tomcat_users:
  - name: admin
    password: 'Boavtug8'
    roles:
      - manager-gui
  - name: john
    password: 'yirphUr7'
    roles:
      - manager-jmx
```

## Dependencies

No dependencies.

## Example Playbook

See test playbook in `/tests/test.yml`

## Contributing

Issues, feature requests, ideas are appreciated and can be posted in the Issues section. Pull requests are also very welcome. Preferably, create a topic branch and when submitting, squash your commits into one (with a descriptive message).

## Contributors

- [Bert Van Vreckem](https://github.com/bertvv) (Initial role)
- [duality72](https://github.com/duality72)

## NOTICE

© 2018 The MITRE Corporation.

Approved for Public Release; Distribution Unlimited. Case Number 18-3678.

## NOTICE
This software was produced for the U. S. Government under Contract Number HHSM-500-2012-00008I, and is subject to Federal Acquisition Regulation Clause 52.227-14, Rights in Data-General.  

No other use other than that granted to the U. S. Government, or to those acting on behalf of the U. S. Government under that Clause is authorized without the express written permission of The MITRE Corporation. 

For further information, please contact The MITRE Corporation, Contracts Management Office, 7515 Colshire Drive, McLean, VA  22102-7539, (703) 983-6000.
