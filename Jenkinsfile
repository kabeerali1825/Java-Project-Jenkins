pipeline {
    agent any

    tools {
         maven 'maven'
         jdk 'java'
         // You may need to configure FindBugs and PMD tools here if not already done in Jenkins global tool configuration
    }

    stages {
        stage('checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'github access', url: 'https://github.com/sreenivas449/java-hello-world-with-maven.git']]])
            }
        }
        
        stage('build') {
            steps {
               echo 'Building...'
               sh 'mvn clean package' // Assuming Maven is used for building
            }
        }
        
        stage('analyze') {
            steps {
                script {
                    // Run FindBugs analysis
                    def findbugsHome = tool 'FindBugs'
                    sh "${findbugsHome}/bin/findbugs -textui -outputFile findbugs-report.html target/*.jar"
                    
                    // Run PMD analysis
                    def pmdHome = tool 'PMD'
                    sh "${pmdHome}/bin/run.sh pmd -d src/main/java -f html -R rulesets/java/quickstart.xml -reportfile pmd-report.html"
                }
                
                // Publish FindBugs and PMD reports
                findBugs pattern: 'findbugs-report.html'
                pmd canComputeNew: false, pattern: 'pmd-report.html'
            }
        }
    }
}
