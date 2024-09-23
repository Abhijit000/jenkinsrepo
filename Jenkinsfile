pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "jenkns-maven"
    }

    stages {
        stage('Checkout') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/jenkins-docs/simple-java-maven-app.git'

              
            }
        }

        stage('Build') {
           steps{
            sh ' mvn clean package'
           }
            
        }

        stage('Test') {
            steps {
             sh 'mvn test'
            }

            post{
               always{
                junit '**/target/surefire-reports/*.xml'
               }   
            }

        }

        stage('Deploy') {

            steps {
                echo 'Deployed ...'
            }
        }

        


        
    }

    post {
    
     failure {
         echo 'Failed!!!!!!!!!!'
          mail to: 'rijudas002@gmail.com'
          subject: "FAILED: ${env.JOB_NAME} - BUILD # ${env.BUILD_NUMBER}"
          body: "URL - ${env.BUILD_URL}"
     }

     success {

        echo "Success...."
        archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false, onlyIfSuccessful: true
     }

    }
}
