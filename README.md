# Ansible role `tomcat`

An Ansible role for setting up and hardening Tomcat on RHEL/CentOS 7 or Fedora. Specifically, the responsibilities of this role are to:

- Install packages from the EPEL repository (EL7: Tomcat 7, Fedora 23: Tomcat 8)
- Manage configuration
- Harden Tomcat install

The firewall configuration is not a concern of this role. Use another role for that (e.g. [bertvv.rh-base](https://galaxy.ansible.com/bertvv/rh-base))

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
