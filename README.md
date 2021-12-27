# Rundeck

Installs and configures Rundeck on EL 8.

This role installs Java 11, and wget as a requirement for Rundeck.

This role currently install the latest version available:

```yaml
rundeck_version: 3.4.9
rundeck_release_date: 20211221
```

This release mitigates the Log4j vulernability. 
