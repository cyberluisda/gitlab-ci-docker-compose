# gitlab-ci-docker-compose
Simple gitlab with gitlab-runner based on docker compose

# Manual start-up of pipeline

**NOTE** see gitlab documentation for each tasks needed to be done per step.

1. Starts gitlab.

   ```bash
   docker-compose up -d gitlab
   ```

   First time gitlab can delay some time while setup all environment

1. Browse to [gitlab local page](http://localhost:9080), change root password
   and optionally create new user.

1. Load _Gitlab runner token_ we will add this in next steps

1. Start gitlab-runner

   ```bash
   docker-compose up -d gitlab-runner
   ```

   With this execution `gitlab-runner` up but can not start properly.
   **Registration is needed**

1. Register `gitlab-runner` in parallel while service is running

  ```bash
  docker-compose exec gitlab-runner /bin/bash
  ```

  Run _registre runner_ into container, and fill data.

  ```bash
  gitlab-runner register
  ```

  Example of fields filled:

  ```
  Running in system-mode.

  Please enter the gitlab-ci coordinator URL (e.g. https://gitlab.com/):
  [http://gitlab/ci]:
  Please enter the gitlab-ci token for this runner:
  [JtW9fB2zJcJ_yAhxiuz6]:
  Please enter the gitlab-ci description for this runner:
  [alpine_docker]:
  Please enter the gitlab-ci tags for this runner (comma separated):
  docker,alpine,dind,did
  Whether to run untagged builds [true/false]:
  [false]: true
  Whether to lock the Runner to current project [true/false]:
  [true]: true
  Registering runner... succeeded                     runner=JtW9fB2z
  Please enter the executor: docker-ssh+machine, kubernetes, docker-ssh, shell, ssh, docker+machine, docker, parallels, virtualbox:
  [docker]: docker
  Please enter the default Docker image (e.g. ruby:2.1):
  [alpine:latest]:
  Runner registered successfully. Feel free to start it, but if it's running already the config should be automatically reloaded!
  ```

If all steps had no errors, now you can run ci pipeline
