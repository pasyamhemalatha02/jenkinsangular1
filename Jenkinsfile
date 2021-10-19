pipeline {

  tools {
    nodejs 'Node16'
  }
    agent any
    stages {
        stage('Check version') {
            steps {
                echo 'Cleaning..'
               
            }
        }
        stage('Install dependencies') {
            steps {
                echo 'Install deps..'
                bat 'npm install'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                bat 'npm test'
            }
        }
        stage('Package') {
            steps {
                echo 'npm run build'
            }
        }

        stage("Deploy to AWS"){
            steps{
                 withAWS(credentials:'puneetawscred', region:'us-east-1') {
                     s3Upload(workingDir:'dist/my-workout-app', includePathPattern:'**/*', bucket:'my-jenkinsangular1', path:'')
            }
            }
            post {
                success{
                    bat 'echo "Uploaded to AWS"'
                }
                failure{
                    bat 'echo "failure"'
                }
            }
        
        }
    }
}
