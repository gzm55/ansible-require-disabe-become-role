require_disabe_become (2.0.0-dev)
=================================

Some ansible tasks is designed to run actions NOT via become,
even if the inventory set `ansible_become=True`.
So this role will try to override some `ansible_become.*` variables to force disable become.

When this role fails:
- with `-e ansible_become=True` in cli parameters, and
- with `-e ansible_become_user=xxx` in cli parameters or `become_allow_same_user` is set to true in some effective ansible.cfg.

Requirements
------------

Python modules:
- ansible>=2.8
- jinja2>=2.7

Role Variables
--------------

N/A

Dependencies
------------

N/A

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
      - { role: gzm55.require_disabe_become }
      - { role: gzm55.local_id_plugin }
      tasks:
      - name: a non-become task
        ping:
        become: False
        become_user: "{{ ansible_user | d(lookup('id', 'euname'), True) }}"
        vars:
          ansible_become: False
          ansible_become_user: "{{ ansible_user | d(lookup('id', 'euname'), True) }}"

TODO
----

Could disable become via overriding the `ansible_become_exe` variable.

License
-------

BSD
