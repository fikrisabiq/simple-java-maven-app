node {
    stage('Checkout') {
        checkout scm
    }

    docker.image('maven:3.9-amazoncorretto-21-debian').inside('-u 0 -v /root/.m2:/root/.m2') {
        stage('Build') {
            sh 'mvn -B -DskipTests clean package'
        }

        stage('Test') {
            try {
                sh 'mvn test'
            } finally {
                junit 'target/surefire-reports/*.xml'
            }
        }

        stage('Deliver') {
            sh 'chmod +x ./jenkins/scripts/deliver.sh && ./jenkins/scripts/deliver.sh'
        }
    }
}