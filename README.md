# Rundeck

Installs and configures Rundeck on EL 8.

This role installs Java 11, and wget as a requirement for Rundeck.

This role currently install the latest version available:

```yaml
rundeck_version: 3.4.9
rundeck_release_date: 20211221
```

This release mitigates the Log4j vulernability.

Installation directory:
```yaml
rundeck_rdeckbase: /opt/rundeck
```

Java memory settings:
```yaml
rundeck_xmx: 4096
rundeck_xms: 256
rundeck_maxmetaspacesize: 128
```

IP configuration:
```yaml
rundeck_port: 4440
rundeck_address: "{{ ansible_all_ipv4_addresses[0] | default('127.0.0.1') }}"
```

Context:
```yaml
# you can change the context to for example: "/rundeck". An empty value means
# that no specific context is added
rundeck_server_web_context: ""
```

Specific rundeck configuration:
```
rundeck_config:
  - parameter: server.address
    value: "{{ rundeck_address }}"
  - parameter: grails.serverURL
    value: "{{ rundeck_url }}"
  - parameter: dataSource.url
    value: "jdbc:h2:file:/opt/rundeck/server/data/grailsdb;MVCC=true"
#   to connect to MySQL, use these settings. (Database has to be prepared.)
```

Settings for rundeck:
```yaml
# stored in: {{ rundeck_rdeckbase }}/etc/framework.properties
rundeck_framework:
  - parameter: framework.server.hostname
    value: "{{ ansible_fqdn }}"
  - parameter: framework.server.name
    value: "{{ ansible_hostname }}"
  - parameter: framework.projects.dir
    value: "{{ rundeck_rdeckbase }}/projects"
  - parameter: framework.var.dir
    value: "{{ rundeck_rdeckbase }}/var"
  - parameter: framework.logs.dir
    value: "{{ rundeck_rdeckbase }}/var/logs"
  # - parameter: "framework.server.username"
  #   value: unset
  # - parameter: "framework.server.password"
  #   value: unset
  - parameter: framework.rundeck.url
    value: "{{ rundeck_url }}"
  # - parameter: "framework.ssh.keypath"
  #   value: unset
  # - parameter: "framework.ssh.user"
  #   value: unset
  - parameter: framework.ssh-connect-timeout
    value: 0
  - parameter: framework.ssh-command-timeout
    value: 0
  # - parameter: "framework.log.dispatch.console.format"
  #   value: unset
  - parameter: framework.rundeck.execution.script.tokenexpansion.enabled
    value: 'yes'
```

Users:
```yaml
rundeck_users:
  - username: "admin"
    password: "admin"
    roles: "user,admin"
  - username: "user"
    password: "user"
    roles: "user"
```

Set plugins with:
```yaml
rundeck_plugins: []
```
