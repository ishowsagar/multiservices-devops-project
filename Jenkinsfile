pipeline {
    // agent specification
    agent any

    // stages specification - pipeline runs each stage
    stages {
      // 1. stage ("name") { steps{..} } - need paranthesis ("for writing stage name")
        stage ("clean start") {
            // what it will do as a job - steps {}
            steps {
              // sh - run these commands
                cleanWs()
                // cleans the workspace before starting anything
              }
          }

      // rest stage's
        stage ("checkout code from SCM") {
            steps {
              // pulls source repo from github by using access token
                git (
                  // note - use commas to seperate key: 'val', pairs when defined horizontally same line but if wrapped then can be only used to seperate each line by putting comma in the end
                    branch: 'main',
                    // id in credentials is -> under which idName this secret would stored to ref in the jenkins file
                    // username is just github usrname
                    credentialsId: 'github-login-token-id', // must store this secret in jenkins first to pull repo
                    url: 'git@github.com:ishowsagar/multiservices-devops-project.git'  // ssh pull format is => git@github.com:usr/repo.git tracker
                // no trailing (ending) comma before closing wrapper
                )
              }
          }
      }

  }
