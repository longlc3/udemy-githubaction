# udemy-githubaction
# use below command to trigger repository_dispatches which uses for trigger other repository
```cmd
curl -L \
  -X POST \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer <YOUR-TOKEN>"\
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/repos/OWNER/REPO/dispatches \
  -d '{"event_type":"on-demand-test","client_payload":{"unit":false,"integration":true}}'
```

# condition 
```yml
name: example-workflow
on: [push]
jobs:
  production-deploy:
    if: github.repository == 'octo-org/octo-repo-prod'
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: '14'
      - run: npm install -g bats
      - name: condition check
        if: $env.allowDeploy == true # if: always() # if: failure() ..
```
- can use needs: [other job, another job]  to decide which job should run first
- or continue-on-error: true
- timeout-minutues: 360

# Stratergy
- different environment, os , node version ...
