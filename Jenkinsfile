pipeline {
   agent { 
        docker {
            image 'mcr.microsoft.com/playwright:v1.48.1-noble'
            args '-v /c/ProgramData/Jenkins/.jenkins/workspace/jenkins-github-actions/:/workspace'
        }
    }
   environment {
      CI = 'true'
   }
   stages {
      stage('install dependencies') {
        steps {
            sh 'npm install'
        }
      }
      stage('e2e-tests') {
        steps {
            sh 'npm ci'
            sh 'npx playwright test'
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
