pipeline{
    agent any
    stages{
        stage('init'){
            steps{
                    echo 'Initilization of building artifacts'
                    sh '''
                    echo "$MAVEN_HOME"
                    '''
            }
        }
        stage('Build'){
            steps{
                echo "Bulding starts here"
                sh 'mvn -v'
            }
        //     post{
        //         success{
        //             echo "Now archiving"
        //             archiveArtifacts artifacts: '**/target/*.war'
        //         }
                
        //     }
        }
        stage('Deploy'){
            steps{
                echo "Check artifacts and its date"
            }
        }
        
    }
}