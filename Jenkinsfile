node {
    docker.image('node:16-buster-slim').inside('-p 3000:3000') {
        triggers {
        pollSCM('H/2 * * * *')
    }
        stage('Build') {
            sh 'npm install'
        }
        stage('Test') {
            if (env.BRANCH_NAME == 'main') {
                sh './jenkins/scripts/test.sh'
            } else {
                echo 'Skipping tests for non-main branches'
            }
        }
    }
}