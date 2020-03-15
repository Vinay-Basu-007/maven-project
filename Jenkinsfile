pipeline{
     agent any
    stages{
        stage('build'){
            steps{
                echo "building..."
                bat 'mvn clean package'
            }
            post{
                success{
                    echo "Now Archiving"
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }

        }
         stage('Deploy to Staging'){
            steps{
                build job: 'deploy-to-stageenv'
            }
        }
        
        stage('Deploy to Production')
        {
            steps{
                timeout(time:5, unit: 'DAYS'){
                    input message: 'Approve PRODUCTION DEPLOYMENT?'
                }
                build job: 'deploy-to-prodenv'
            }
            post{
                success{
                    echo 'The PROD build is successful'
                }
                failure{
                    echo 'The deployment to PROD failed'
                }
            
            }
        }
    }

}