pipeline {
   agent any
   environment {
      CI = 'true'
   }
   stages {
      stage('install dependencies') {
        steps {
            bat 'npm install'
        }
      }
   }
   stages {
      stage('e2e-tests') {
        steps {
            bat 'npm ci'
            bat 'npx playwright test'
        }
        post {
            always {
                archiveArtifacts artifacts: 'test-results/**/*', allowEmptyArchive: true
            }
        }
      }
   }
   post {
        always {
            cleanWs()
        }
   }
}
