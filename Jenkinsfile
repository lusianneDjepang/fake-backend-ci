/* import shared library */
@Library('jenkins-shared-library')_

pipeline {
    agent none
    stages {
        /*stage('Check Goland syntax') {
            agent { docker { image 'golangci/golangci-lint' } }
            steps {
                sh 'cat \${WORKSPACE}/fake-backend/config.go'
                sh 'golangci-lint run \${WORKSPACE}/fake-backend/config.go'
            }
        }*/
        stage('Check docker-compose syntax') {
            agent { docker { image 'docker/compose' } }
            steps {
                sh 'docker-compose -f \${WORKSPACE}/docker-compose.yml config'
            }
        }
        stage('Check Dockerfile syntax') {
            agent { docker { image 'hadolint/hadolint' } }
            steps {
                sh 'hadolint \${WORKSPACE}/Dockerfile'
            }
        }
    }
    post {
    always {
       script {
         /* Use slackNotifier.groovy from shared library and provide current build result as parameter */
         clean
         slackNotifier currentBuild.result
     }
    }
    }
}
