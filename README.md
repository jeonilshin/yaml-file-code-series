# buildspec.yaml
```
version: 0.2

phases:
  pre_build:
    commands:
      - <commands>
  build:
    commands:
      - <commands>
  post_build:
    commands:
      - <commands>
artifacts:
  files:
    - 'appspec.yml'
```
# appspec.yaml
```
version: 0.0
os: linux
files:
  - source: /
    destination: /var/www/html/WordPress
hooks:
  BeforeInstall:
    - location: scripts/install_dependencies.sh
      timeout: 180
      runas: root
  AfterInstall:
    - location: scripts/change_permissions.sh
      timeout: 180
      runas: root
  ApplicationStart:
    - location: scripts/start_server.sh
    - location: scripts/create_test_db.sh
      timeout: 180
      runas: root
  ApplicationStop:
    - location: scripts/stop_server.sh
      timeout: 180
      runas: root

```
