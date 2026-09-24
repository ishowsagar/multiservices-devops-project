pipeline {
    // agent specification
    agent any 

    // stages specification - pipeline runs each stage 
    stages {
      // 1. stage "name"  
        stage "clean start" {
            // what it will do as a job - steps {}
            steps {
              // sh - run these commands 
                cleanWs()
                // cleans the workspace before starting anything
              }
          }

      // rest stage's 
        stage "checkout code from SCM" {
            steps {
              // pulls source repo from github by using access token 
                git branch 'main',
                    credentialsId: 'github-secret-access-token-id' // must store this secret in jenkins first to pull repo
                    url: 'https://github.com/ishowsagar/multiservices-devops-project/'
              }
          }
      }

  }
