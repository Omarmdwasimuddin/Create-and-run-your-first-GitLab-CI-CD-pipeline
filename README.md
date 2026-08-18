# Create and run your first GitLab CI/CD pipeline

## পূর্বশর্ত (Pre-requirement)

- Runner Setup এবং Registration করা থাকতে হবে।
- দেখুন: [GitLab Runner Setup and Registration](https://github.com/Omarmdwasimuddin/Docker-Desktop-Register-GitLab-Runner-with-GitLab-Server)

---

## ধাপ ১: Runner Config ফাইল Edit করা

নিচের ফাইলটি open করে edit করতে হবে:

```
C:\Users\User\Desktop\Demo\gitlab-runner\config\config.toml
```

এই ফাইলে `network_mode = "demo_default"` লাইনটি যোগ করতে হবে।

```toml
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

### Runner Restart করা

**PowerShell-এ চালাতে হবে:**

```bash
docker restart my-gitlab-runner
```

### Restart হয়েছে কিনা যাচাই করা

```bash
docker logs my-gitlab-runner --tail 20
```

---

## ধাপ ২: নতুন Project তৈরি করা

নিচের ধাপগুলো অনুসরণ করতে হবে:

1. Visit করুন: `http://localhost:8000/dashboard/projects`
2. **New project** এ ক্লিক করুন
3. **Create blank project** এ ক্লিক করুন
4. Project name দিন: `My first pipeline`
5. Project URL দিন
6. Visibility Level সিলেক্ট করুন: `public`
7. **Create project** এ ক্লিক করুন

<img width="1546" height="801" alt="Create blank project screenshot" src="https://github.com/user-attachments/assets/ffee2040-1e27-40c5-9d7e-a9ed2177f699" />

---

## ধাপ ৩: `.gitlab-ci.yml` ফাইল তৈরি করা

1. বামের sidebar-এ যান: **Code > Repository**
2. উপরে ডানদিকে `+` আইকনে ক্লিক করে **New file** সিলেক্ট করুন
3. Filename এ লিখুন: `.gitlab-ci.yml`
4. নিচের code টি paste করুন:

```yaml
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

এই pipeline-এ মোট ৩টি stage আছে: `build`, `test`, এবং `deploy`।

---

## ধাপ ৪: Pipeline দেখা ও যাচাই করা

### Pipeline List দেখা

**Build > Pipelines**-এ যান। এখানে ৩টি stage সহ একটি pipeline দেখা যাবে:

<img width="1269" height="155" alt="Pipeline list with three stages" src="https://github.com/user-attachments/assets/ca244bd9-8ea4-4876-8097-3841034a6b31" />

### Pipeline-এর Visual Representation দেখা

Pipeline ID-তে ক্লিক করলে (উদাহরণস্বরূপ `#2435445330`) visual representation দেখা যাবে:

<img width="927" height="445" alt="Pipeline visual representation" src="https://github.com/user-attachments/assets/8c30af98-ff59-4f8a-8241-30ffc760dec2" />

### নির্দিষ্ট Job-এর Details দেখা

Job name-এ ক্লিক করলে সেই job-এর details দেখা যাবে। উদাহরণস্বরূপ `deploy-prod`:

<img width="984" height="706" alt="deploy-prod job details" src="https://github.com/user-attachments/assets/46d12bca-5af8-492c-a2fb-5aadc6175870" />

---

## সম্পন্ন! 🎉

আপনি সফলভাবে GitLab-এ আপনার প্রথম CI/CD pipeline তৈরি করে ফেলেছেন। Congratulations!
