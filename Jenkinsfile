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
                        steps{
                            echo 'Hello'                        
                        }
                    }
                }
            }
            stage('release'){
                when{
                    allOf{
                        branch 'release/*'
                }
            }
            stages{
                stage('Validate_Against_QA'){
                        steps{
                            echo 'This is QA Branch'
                            sh 'git --version'                       
                        }
                    }
                }
            }
       
        }
    }
