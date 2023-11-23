pipeline{
    agent any
    stages {
        stage('Build'){
            steps{
                withMaven{
                    sh 'mvn -B -DskipTests clean package'
                }
            }
        }
        stage('Test'){
            steps{
                withMaven{
                    sh 'mvn test'
                }
            }
            post{
                always{
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Sonar Analysis'){
            steps{
                script{
                    def scannerHome = tool 'SonarScanner 4.0';
                    withSonarQubeEnv('SonarCloud') {
                        sh "${scannerHome}/bin/sonar-scanner"
                    }
                }   
            }
        }
    }
}