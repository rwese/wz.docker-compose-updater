wz.docker-compose-updater
=========

Setup a service for periodic, *daily*, pull/updates of docker-compose's.

This is usually added to an docker-compose project's role to be triggered alongside the role.

Requirements
------------

Nothing

Role Variables
--------------

| `docker_compose_updater__project_name` | String | the projectname, if set, usually fallsback to directory | `'docker-compose-super-project'` | Yes |
| `docker_compose_updater__target_path` | String | location of the docker-compose project | `/opt/docker-compose-project` | Yes |
| `docker_compose_updater__state` | String | State of the updater | `present|absent` | No |
| `docker_compose_updater__custom_script` | String | Can be used for services which require post update setups to run (e.g. nextcloud needs `occ upgrade` to be run) | `/root/some_post_update_tasks.sh` | No |

Dependencies
------------


Example Playbook
----------------

This role is more meant to be added to an role but can be also used to install an updater for exiting docker-composes.

    - hosts: servers
      roles:
         - role: wz.docker-compose-updater,
           vars:
            docker_compose_updater__project_name: 'docker-compose-project'
            docker_compose_updater__target_path: '/opt/docker-compose-project'
            docker_compose_updater__state: 'present'

Example Role Task
-----------------

  - name: trigger docker-compose-updater role
    include_role:
      name: wz.docker-compose-updater
    vars:
      docker_compose_updater__project_name: "{{ docker_compose_project__project_name }}"
      docker_compose_updater__target_path: "{{ docker_compose_project__target_path }}"
      docker_compose_updater__state: "{{ docker_compose_project__state|default('present') }}"


License
-------

MIT

Author Information
------------------

