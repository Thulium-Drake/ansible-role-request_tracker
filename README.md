## Request Tracker, powered by Ansible
This role provides a means to install BestPractical Request tracker on your system.

It requires:

- Debian 11 with backports enaled or RHEL(-like) 9
- A MySQL database server already set up
- Internet access (Github, CPAN and distro repos)

This role has a soft dependency on using https://github.com/Thulium-Drake/ansible-role-apache_revproxy to provide the webserver. Add the following configuration to your host_vars:

```
apache_apps:
  - name: "{{ ansible_facts['fqdn'] }}"
    type: 'rt5'
    cert: "/etc/ssl/{{ ansible_facts['fqdn'] }}/{{ ansible_facts['fqdn'] }}.crt"
    key: "/etc/ssl/{{ ansible_facts['fqdn'] }}/{{ ansible_facts['fqdn'] }}.key"
    hsts: false
    state: 'present'
```

And this to your requirements:

```
- name: 'apache_revproxy'
  src: 'thulium_drake.apache_revproxy'
```

However, if you have your own means of providing a Apache webserver, you can also use that.
