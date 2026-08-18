# Create and run your first GitLab CI/CD pipeline

> ## Pre-requirement
>  - Runner Setup and Registration kora thakte hobe.
>  - See [GitLab Runner Setup and Registration](https://github.com/Omarmdwasimuddin/Docker-Desktop-Register-GitLab-Runner-with-GitLab-Server)


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
<img width="1626" height="302" alt="image" src="https://github.com/user-attachments/assets/d93bf9bb-0c4e-451d-9f29-d1ceb8185847" />

#### View a visual representation of your pipeline by selecting the pipeline ID (#2435445330 in this example):
<img width="927" height="445" alt="image" src="https://github.com/user-attachments/assets/8c30af98-ff59-4f8a-8241-30ffc760dec2" />

#### View details of a job by selecting the job name. For example, deploy-prod:
<img width="1858" height="1240" alt="image" src="https://github.com/user-attachments/assets/a03c1eb8-4d51-4335-a12b-46c330c9cfe2" />

> You have successfully created your first CI/CD pipeline in GitLab. Congratulations!
