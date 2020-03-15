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
    }


}