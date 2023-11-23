pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        withMaven() {
          sh 'mvn -B -DskipTests clean package'
        }

      }
    }

    stage('Test') {
      post {
        always {
          junit 'target/surefire-reports/*.xml'
        }

      }
      steps {
        withMaven() {
          sh 'mvn test'
        }

      }
    }

    stage('Sonar Analysis') {
      steps {
        script {
          def scannerHome = tool 'SonarScanner 4.0';
          withSonarQubeEnv('SonarCloud') {
            sh "${scannerHome}/bin/sonar-scanner"
          }
        }

      }
    }

  }
}