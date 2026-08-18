# Create and run your first GitLab CI/CD pipeline

> ## Pre-requirement
>  - Runner Setup and Registration kora thakte hobe.
>  - See [GitLab Runner Setup and Registration](https://github.com/Omarmdwasimuddin/Docker-Desktop-Register-GitLab-Runner-with-GitLab-Server)


> #### C:\Users\User\Desktop\Demo\gitlab-runner\config\config.toml  ---> file open kore edit koro
> add koro `network_mode = "demo_default"`
```bash
concurrent = 1
check_interval = 0
shutdown_timeout = 0

[session_server]
  session_timeout = 1800

[[runners]]
  name = "my-docker-runner"
  url = "http://my-gitlab-server"
  id = 1
  token = "glrtr-NABy5HTJzrEsdJecko-D"
  token_obtained_at = 2026-08-12T00:50:31Z
  token_expires_at = 0001-01-01T00:00:00Z
  executor = "docker"
  [runners.cache]
    MaxUploadedArchiveSize = 0
    [runners.cache.s3]
      AssumeRoleMaxConcurrency = 0
    [runners.cache.gcs]
    [runners.cache.azure]
  [runners.docker]
    tls_verify = false
    image = "alpine:latest"
    privileged = false
    disable_entrypoint_overwrite = false
    oom_kill_disable = false
    disable_cache = false
    volumes = ["/cache"]
    volume_keep = false
    shm_size = 0
    network_mtu = 0
    network_mode = "demo_default"
```
---


#### visit: http://localhost:8000/dashboard/projects ---> click: New project ---> click: Create blank project ---> Project name: My first pipeline ---> Project URL daw ---> Visibility Level: public ---> click: Create project
<img width="1546" height="801" alt="image" src="https://github.com/user-attachments/assets/ffee2040-1e27-40c5-9d7e-a9ed2177f699" />



> #### `.gitlab-ci.yml` ফাইল বানানো
> - বামের সাইডবারে Code > Repository
> - উপরে ডানদিকে + আইকনে ক্লিক করে New file
> - Filename এ লিখো: `.gitlab-ci.yml`
> - নিচের কোড পেস্ট করো:
```bash
build-job:
  stage: build
  tags:
    - docker
  script:
    - echo "Hello, $GITLAB_USER_LOGIN!"

test-job1:
  stage: test
  tags:
    - docker
  script:
    - echo "This job tests something"

test-job2:
  stage: test
  tags:
    - docker
  script:
    - echo "This job tests something, but takes more time than test-job1."
    - sleep 20

deploy-prod:
  stage: deploy
  tags:
    - docker
  script:
    - echo "This job deploys something from the $CI_COMMIT_BRANCH branch."
  environment: production
```
---


#### Go to Build > Pipelines. A pipeline with three stages should be displayed:
<img width="1269" height="155" alt="image" src="https://github.com/user-attachments/assets/ca244bd9-8ea4-4876-8097-3841034a6b31" />

#### View a visual representation of your pipeline by selecting the pipeline ID (#2435445330 in this example):
<img width="927" height="445" alt="image" src="https://github.com/user-attachments/assets/8c30af98-ff59-4f8a-8241-30ffc760dec2" />

#### View details of a job by selecting the job name. For example, deploy-prod:
<img width="984" height="706" alt="image" src="https://github.com/user-attachments/assets/46d12bca-5af8-492c-a2fb-5aadc6175870" />

> You have successfully created your first CI/CD pipeline in GitLab. Congratulations!
