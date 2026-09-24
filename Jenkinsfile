pipeline {
    // agent specification
    agent any

    // env variables -> shipped inside stages
    environment {
      // key='val', it also comes with many built-in vars like BUILD_NUMBER, used as ${env.BUILD_NUMBER}, even custom var as ${env.key}
      backendImg = 'backend-img:' //eg backend-img:v1 ( if build no is 1)
      frontendImg = 'frontend-img'
    
    }
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
          stage ("Source code verfication") {
            steps {
              // after cloning repo, it -> cd into cloned repo before entering next stage, so we are already inside repo which is being saved at
              // var//jenkins_home/workspace/jenkins-pipeline(ig). 
              sh 'ls -ltr'
              sh 'echo "verification is successfull!" '
            }
          }

          // 4. stage - build all images
          stage ("Build Backend Image") {
            steps {
              // don't need to specify file for building image just need to provide dir path being . or ./else or -f for specifying the docker file
              // note - must use double quotes for shell commands when used with variables for var interpolation
              sh "docker build -f ./backend/dockerfile -t ${env.backendImg}:v${env.BUILD_NUMBER} ./backend"
              sh 'docker image ls | grep backend'
            }
          } 

          stage ("Build Frontend Image") {
            steps {
              // important - sh space_needed "" dble-quotes for injecting vars and recognition
              sh "docker build -f ./frontend/dockerfile -t ${env.frontendImg}:v${env.BUILD_NUMBER} ./frontend"
              sh 'docker image ls | grep frontend'
            }
          } 

          // 5. stage - images cleanup  
          stage ("Multiservices Images Cleanup") {
            steps {
              // triple quotes for multi line non-break sh
              // single if non-var,double if var
              sh """
                docker rmi ${env.backendImg}:v${env.BUILD_NUMBER}
                docker rmi ${env.frontendImg}:v${env.BUILD_NUMBER}
              """
            }
          }

          // 6. stage - built images post cleanup checkup 
          stage ("Pipeline Cleanup check") {
            steps {
              sh 'docker image ls'
            }
          }
      }

  }
