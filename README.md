ajgarlag.deploy
===============

Ansible role to deploy applications heavily inspired by [ansistrano](https://github.com/ansistrano/deploy).

Role Variables
--------------

* **ajgarlag_deploy_path**: Path where the code is going to be deployed to (defaults to `{{ansible_env.HOME}}/project`).
* **ajgarlag_deploy_update_strategy**: Strategy to update code on hosts (defaults to `git`).
* **ajgarlag_deploy_update_git_repo**: GIT repository (required if the update strategy is `git`).
* **ajgarlag_deploy_update_git_commit**: GIT commit to deploy (defaults to `master`).
* **ajgarlag_deploy_update_git_cache**: Boolean flag to cache the remote GIT repository for faster deployments (defaults to `yes`).
* **ajgarlag_deploy_update_artifact_location**: URL or absolute path where the artifact is located (required if the update strategy is `artifact`).
* **ajgarlag_deploy_symlink_shared**: Array shared paths (defaults to `[]`).
* **ajgarlag_deploy_symlink_forced**: Boolean flag to force the creation of symlinks for shared paths (defaults to `no`).
* **ajgarlag_cleanup_keep**: Number of releases to keep in your hosts, if 0, unlimited releases will be kept (defaults to `5`).

### Role hooks

You can hook your own tasks files to the deployment process defining any of the following vars:

* **ajgarlag_deploy_before_setup_tasks_file**
* **ajgarlag_deploy_after_setup_tasks_file**
* **ajgarlag_deploy_before_update_tasks_file**
* **ajgarlag_deploy_after_update_tasks_file**
* **ajgarlag_deploy_before_symlink_shared_tasks_file**
* **ajgarlag_deploy_after_symlink_shared_tasks_file**
* **ajgarlag_deploy_before_symlink_tasks_file**
* **ajgarlag_deploy_after_symlink_tasks_file**
* **ajgarlag_deploy_before_cleanup_tasks_file**
* **ajgarlag_deploy_after_cleanup_tasks_file**

To do it, you must define the desired var with the path to the tasks file:

```yml
ajgarlag_deploy_before_update_tasks_file: "{{ playbook_dir }}/tasks/before_update.yml"
```


Example Playbook
----------------

```yml
- hosts: all
  vars:
    ajgarlag_deploy_path: /var/www/application
    ajgarlag_deploy_update_git_repo: https://example.org/sample/application.git
    ajgarlag_deploy_symlink_shared:
    - config.yml
    - logs
    - uploads
  roles:
    - role: ajgarlag.deploy
```

License
-------

MIT

Author Information
------------------

Developed with ♥ by [Antonio J. García Lagar](http://aj.garcialagar.es).
