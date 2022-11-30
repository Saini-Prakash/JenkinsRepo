pipeline
    {
        agent any
        stages{
            stage(feature){
                when{
                    allof{
                        branch 'feature/*'
                }
            }
            stages{
                stage('Validate_Against_Dev'){
                    agent any{
                        steps{
                            echo 'Hello'
                            sh 'git config http.sslVerify "false"'
                        }
                    }
                }
            }
            }
            
        }
    }
