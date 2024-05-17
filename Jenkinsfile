pipeline
    {
        agent any
        stages{
            stage(feature){
                when{
                    allOf{
                        branch 'feature/*'
                }
            }
            stages{
                stage('Validate_Against_Dev'){
                    agent any
                        steps{
                            echo 'Hello'
                            sh 'git config http.sslVerify "false"'
                        
                    }
                }
            }
            }
            stage(SIT){
                when{
                    allOf{
                        branch 'SIT/*'
                }
            }
            stages{
                stage('Validate_Against_SIT'){
                    agent any
                        steps{
                            echo 'Hello'
                            sh 'git config http.sslVerify "false"'
                        
                    }
                }
            }
            }
            
        }
    }
