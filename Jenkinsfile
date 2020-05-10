pipeline{
    agent any

    tools{
        maven "M2"

    }
    stages{
        stage('init'){
            steps{
                    echo 'Initilization of building artifacts'
            }
        }
        stage('Build'){
            steps{
                echo "Bulding starts here"
                sh 'mvn clean package'
            }
            post{
                success{
                    echo "Now archiving"
                    archiveArtifacts artifacts: '**/target/*.war'
                }
                
            }
        }
        stage('Deploy to stage'){
            steps{
                echo "deploy to stage"
                build job: 'deploy-to-stage'
            }
        }
    }
}