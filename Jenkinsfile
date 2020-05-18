pipeline {
    agent any

    parameters {
         string(name: 'tomcat_test', defaultValue: '52.14.63.12', description: 'Staging Server')
         string(name: 'tomcat_prod', defaultValue: '18.218.125.65', description: 'Production Server')
    }
    tools{
        maven "M2"

    }

stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage("Method 2 ssh") {
	        steps {
		        sshagent (credentials: ['creds-id']) {
		        sh '''
                    scp -i /home/ec2-user/.ssh/id_rsa **/target/*.war ec2-user@${params.tomcat_test}:/home/ec2-user/apache-tomcat-8.5.54/webapps/
                    scp -i /home/ec2-user/.ssh/id_rsa **/target/*.war ec2-user@${params.tomcat_prod}:/home/ec2-user/apache-tomcat-8.5.54/webapps/
		        '''
		        }
	        }
        }
        // stage ('Deployments'){
        //     parallel{
        //         stage ('Deploy to test'){
        //             steps {
        //                 sh "scp -i /home/ec2-user/.ssh/id_rsa **/target/*.war ec2-user@${params.tomcat_test}:/home/ec2-user/apache-tomcat-8.5.54/webapps/"
        //             }
        //         }

        //         stage ("Deploy to Production"){
        //             steps {
        //                 sh "scp -i /home/ec2-user/.ssh/id_rsa **/target/*.war ec2-user@${params.tomcat_prod}:/home/ec2-user/apache-tomcat-8.5.54/webapps/"
        //             }
        //         }
        //     }
        // }
    }
}