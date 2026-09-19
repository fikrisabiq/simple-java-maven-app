node {
    def mavenImg = docker.image('maven:3.9-amazoncorretto-21-debian')
    def dockerArgs = '-u 0:0 -v /root/.m2:/root/.m2'

    try {
        stage('Checkout') {
            checkout scm
        }

        stage('Build') {
            mavenImg.inside(dockerArgs) {
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            mavenImg.inside(dockerArgs) {
                sh 'mvn test'
            }
        }

        stage('Manual Approval') {
            input message: 'Lanjutkan ke tahap Deploy?', ok: 'Proceed'
        }

        stage('Deploy') {
            sh 'chmod +x jenkins/scripts/deliver.sh'
            sh './jenkins/scripts/deliver.sh'
            
            sleep time: 1, unit: 'MINUTES'
        }
    } finally {
        sh 'chmod -R 777 target/ || true'
    }
}