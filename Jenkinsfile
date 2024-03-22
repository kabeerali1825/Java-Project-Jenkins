pipeline {
    agent any

    tools {
        maven 'maven'
        jdk 'java'
    }

    stages {
        stage('checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'github access', url: 'https://github.com/sreenivas449/java-hello-world-with-maven.git']]])
            }
        }
        
        stage('build') {
            steps {
                echo 'Building the project...'
                sh 'mvn clean install'
            }
        }

        stage('findbugs') {
            steps {
                echo 'Running FindBugs...'
                sh 'mvn findbugs:findbugs'
            }
        }

        stage('pmd') {
            steps {
                echo 'Running PMD...'
                sh 'mvn pmd:pmd'
            }
        }
    }
}
