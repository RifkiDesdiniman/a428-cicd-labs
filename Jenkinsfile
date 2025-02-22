node {
    // Menambahkan Poll SCM sebagai Build Trigger setiap 2 menit
    properties([
        pipelineTriggers([
            pollSCM('H/2 * * * *')
        ])
    ])

    docker.image('node:16-buster-slim').inside('-p 3000:3000') {
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
