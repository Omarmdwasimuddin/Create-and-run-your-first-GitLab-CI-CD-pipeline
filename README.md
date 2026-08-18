# Create and run your first GitLab CI/CD pipeline

> ## Pre-requirement
>  - Runner Setup and Registration kora thakte hobe.
>  - See [GitLab Runner Setup and Registration](https://github.com/Omarmdwasimuddin/Docker-Desktop-Register-GitLab-Runner-with-GitLab-Server)

#### .gitlab-ci.yml
```bash
build-job:
  stage: build
  script:
    - echo "Hello, $GITLAB_USER_LOGIN!"

test-job1:
  stage: test
  script:
    - echo "This job tests something"

test-job2:
  stage: test
  script:
    - echo "This job tests something, but takes more time than test-job1."
    - sleep 20

deploy-prod:
  stage: deploy
  script:
    - echo "This job deploys something from the $CI_COMMIT_BRANCH branch."
  environment: production
```
---
