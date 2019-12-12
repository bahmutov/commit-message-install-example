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

## Note

When you halt a job it is considered successfully finished. Thus in a workflow, the jobs that follow will start running. If you really want to halt everything, make this utility into a command and halt _each job_.
