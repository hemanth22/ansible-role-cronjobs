cronjobs
=========

ansible role cronjobs created to integrate with rundeck for deployment and rollback

Requirements
------------

Ensure crontab, diff, sdiff is installed.


Role Variables
--------------

Below is the default roles variable

```yaml
---
backup_dir: "/tmp/{{ CHANGE_ID }}"
CHANGE_ID: "{{ lookup('env', 'CHANGE_ID') | default('CHG123456789', True) }}"
CRON_MINUTE: "{{ lookup('env', 'CRON_MINUTE') | default('*', True) }}"
CRON_HOUR: "{{ lookup('env', 'CRON_HOUR') | default('0', True) }}"
CRON_DAY: "{{ lookup('env', 'CRON_DAY') | default('*', True) }}"
CRON_MONTH: "{{ lookup('env', 'CRON_MONTH') | default('*', True) }}"
CRON_WEEKDAY: "{{ lookup('env', 'CRON_WEEKDAY') | default('*', True) }}"
CRON_USER: "{{ lookup('env', 'CRON_USER') | default('root', True) }}"
CRON_JOB: "{{ lookup('env', 'CRON_JOB') | default('/usr/bin/date >> /tmp/date_log2.txt', True) }}"
CRON_JOBNAME: "{{ lookup('env', 'CRON_JOBNAME') | default('Log current date every minute', True) }}"
```

Dependencies
------------

No dependency with other roles hosted on Ansible Galaxy.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
---
- hosts: localhost
  gather_facts: false
  become_user: "{{ CRON_USER }}"
  become: true
  roles:
    - hemanth22.cronjobs
```

__Command to execute deploy:__

```bash
ansible-playbook -vvvvv main.yaml  -e "CHANGE_ID=CHG123456788" -e "CRON_MINUTE=*" -e "CRON_HOUR=*" -e "CRON_DAY=*" -e "CRON_MONTH=*" -e "CRON_WEEKDAY=*" -e "CRON_USER=rundeck" -e "CRON_JOB='/usr/bin/date >> /tmp/date_log2.txt'" -e "CRON_JOBNAME='Log current date every minute'" --tags deploy
```

__Command to execute rollback:__

```bash
ansible-playbook -vvvvv main.yaml  -e "CHANGE_ID=CHG123456788" -e "CRON_MINUTE=*" -e "CRON_HOUR=*" -e "CRON_DAY=*" -e "CRON_MONTH=*" -e "CRON_WEEKDAY=*" -e "CRON_USER=rundeck" -e "CRON_JOB='/usr/bin/date >> /tmp/date_log2.txt'" -e "CRON_JOBNAME='Log current date every minute'" --tags rollback
```

License
-------

GPL-3.0-only

Author Information
------------------

This role was created in 2024 by Hemanth BITRA. Author Website: bitroid.in
