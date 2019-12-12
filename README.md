# commit-message-install-example
> See https://github.com/cypress-io/commit-message-install

See [circle.yml](circle.yml) which uses [CircleCI early halt feature](https://circleci.com/docs/2.0/configuration-reference/#ending-a-job-from-within-a-step) to stop the job if there is no commit message JSON

```yml
# install tool locally
- run: npm install @cypress/commit-message-install
- run: |
    if ! $(npm bin)/has-message; then
        echo Stopping early, no commit message
        circleci-agent step halt
    else
        echo All good, found commit message JSON
    fi
```

```yml
# install tool globally using Yarn
- run: yarn global @cypress/commit-message-install
- run: |
    if ! has-message; then
        echo Stopping early, no commit message
        circleci-agent step halt
    else
        echo All good, found commit message JSON
    fi
```
