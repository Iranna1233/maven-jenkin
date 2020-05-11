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
                build job: 'stage-pipeline'
            }
        }
        stage('Deploy to Production'){
            steps{
                echo "deply to production"
                timeout(time:5, unit:"DAYS"){
                    input message:'Approve PRODUCTION Deployment ?'
                }
                build job: 'deploy-to-prod'
            }

            post {
                success {
                    echo "code deployed to producion"
                }

            failure{
                    echo "Deployment Failed"
                }
            }
        }
}
