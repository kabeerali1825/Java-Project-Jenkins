pipeline{
    agent any

    tools {
         maven 'maven'
         jdk 'java'
    }

    stages{
        stage('checkout'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'github access', url: 'https://github.com/sreenivas449/java-hello-world-with-maven.git']]])
            }
        }
        stage('build'){
            steps{
               echo 'success'
            }
        }
        stage('Static Analysis') {
            steps {
                bat 'mvn pmd:pmd'
                bat 'mvn findbugs:findbugs'
            }
        }
    }
    post {
          success {
            echo 'The build was successful!'
           
        }
        failure {
            echo 'The build failed'
            
         }
    }
}
