pipeline {
    agent any
    environment {
        SF_DEPLOY__ENABLED = true
        GIT_USERNAME = credentials('GIT_USERNAME')
        SF_ORG__QA__AUTH_URL = credentials('SF_ORG__QA__AUTH_URL')
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
                        withCredentials([usernamePassword(credentialsId: 'ccadmin', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USER')]) {
                            sh 'git config http.sslVerify "false"'
                            sh 'git config credential.username "${GIT_USER}"'
                            sh(returnStdout: true, script: 'git config credential.helper "!echo password=${GIT_PASSWORD}; echo"')
                            script{
                                fetch_all_tags = sh(script: 'git fetch --tags', , returnStdout: true).trim()
                                qa_tag = sh(script: 'git describe --match "qa-*" --abbrev=0 --tags HEAD', , returnStdout: true).trim()
    
                            }
                            sh "echo $SF_ORG__QA__AUTH_URL > authURLFile"
                            sh "sfdx force:auth:sfdxurl:store -f authURLFile -s -a QA"
                            sh "sfdx sgd:source:delta --from $qa_tag --to HEAD --output . --ignore .packageignore"
                            sh 'echo "--- package.xml generated with added and modified metadata from $qa_tag"'
                            sh "cat package/package.xml"
                            sh "sfdx force:source:deploy -x package/package.xml --checkonly --testlevel NoTestRun"
                            sh 'echo "--- destructiveChanges.xml generated with deleted metadata"'
                            sh "cat destructiveChanges/destructiveChanges.xml"
                            sh "sfdx force:mdapi:deploy -d destructiveChanges --checkonly --ignorewarnings --wait 10"
                        }
                    }
                }
            }
        }
    }
}
