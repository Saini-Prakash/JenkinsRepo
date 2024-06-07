pipeline {
    agent any
    environment {
        SF_DEPLOY__ENABLED = true
        GIT_USERNAME = credentials('GIT_USERNAME')
        SF_ORG__QA__AUTH_URL = credentials('SF_ORG__QA__AUTH_URL')
        Github_URL=credentials('Github_URL')
    }
    stages {
     stage('feature') {
            when {
              allOf{
                branch 'feature/*'
                // changeset "force-app/**"
              }
            }
            stages{
                stage('validate_against_QA'){
                    agent any
                    steps {
                        withCredentials([usernamePassword(credentialsId: 'GIT_USERNAME', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USER')]) {
                            git config http.sslVerify "false"
                            git config credential.username "${GIT_USER}"
                            }
                            echo 'destructiveChanges.xml generated with deleted metadata'

                            echo "--- package.xml generated with added and modified metadata from" 
                        
                    }
                }
            }
        }
    }
}
