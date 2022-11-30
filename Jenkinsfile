pipeline
    {
        agent any
        environment {
        GIT_USERNAME = credentials('GIT_USERNAME')
        SF_ORG_DEV_AUTH_URL = credentials('SF_ORG_DEV_AUTH_URL')
        }
        stages{
            stage('feature'){
                when{
                    allOf{
                        branch 'feature/*'
                }
            }
            stages{
                stage('Validate_Against_Dev'){
                    agent any
                        steps{
                            sh 'echo $GIT_USERNAME'
                            sh 'echo $SF_ORG_DEV_AUTH_URL'
                            echo 'Hello'
                            sh 'git config http.sslVerify "false"'
                        
                    }
                }
            }
            }
            
        }
    }
