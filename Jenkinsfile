def COLOR_MAP = [
    'SUCCESS': 'good', 
    'FAILURE': 'danger',
]
pipeline{
    agent any
    tools {
        maven "MAVEN3.9"
        jdk "JDK17"
    }
    stages{
        stage('Build'){
            steps{
                echo "Hello bapu"
            }
            
        }

        stage('Test'){

            steps{
                echo "Running Tests"
            }
            
        }

        stage("sonarqube code analysis") { 
            environment{
                scannerHome = tool 'sonar6.2'
            } 
            steps {
                  withSonarQubeEnv('sonarserver') {
                  sh '''${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=vprofile \
                   -Dsonar.projectName=vprofile \
                   -Dsonar.projectVersion=1.0 \
                   -Dsonar.sources=src/ \
                   -Dsonar.java.binaries=target/test-classes/com/visualpathit/account/controllerTest/ \
                   -Dsonar.junit.reportsPath=target/surefire-reports/ \
                   -Dsonar.jacoco.reportsPath=target/jacoco.exec \
                   -Dsonar.java.checkstyle.reportPaths=target/checkstyle-result.xml'''
             }
           }
        }

        stage('Deploy'){
            steps{
                echo "Deploying Application"
            }
                
        }
    }
}