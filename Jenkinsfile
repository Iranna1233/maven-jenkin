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
            post{
                success{
                    echo "Copy artifacts from another project"
                    copyArtifacts filter: '**/*.war', fingerprintArtifacts: true, projectName: 'beg_pipeline', selector: lastSuccessful()
                }
            }
        }
        // stage('Post build'){
        //     steps{
        //         echo "Deploy to container"
        //         deploy adapters: [tomcat8(credentialsId: 'a7ad4ea9-4734-4587-bff2-417e61da577a', path: '', url: 'http://3.23.111.102:8090/')], contextPath: 'webap', onFailure: false, war: '**/*.war'
        //     }
        // }
    }
}
