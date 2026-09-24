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
                    // https://github.com/usr/repo.git
                    url: 'https://github.com/ishowsagar/BLOG-WEB-GO-FS-APP.git'  // ssh pull format is => git@github.com:usr/repo.git tracker
                // no trailing (ending) comma before closing wrapper
                )
              }
          }
          // ** worked ** // 

          // 3. stage - dir verification if actually pulled right code - also we changed to clone desired repo other than where our jks file was 
          stage ("k8s dir verfication") {
            steps {
              // after cloning repo, it -> cd into cloned repo before entering next stage, so we are already inside repo which is being saved at
              // var//jenkins_home/workspace/jenkins-pipeline(ig). 
              sh '''
              ls -ltr
              ls | grep "backend"
            '''
            }

          }
      }

  }
