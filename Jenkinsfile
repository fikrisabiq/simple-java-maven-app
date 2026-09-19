node('!windows') {
    stage('Checkout') {
        checkout scm
    }

    stage('Build') {
        sh 'mvn -B -DskipTests clean package'
    }

    stage('Test') {
        try {
            sh 'mvn test'
        } finally {
            // Menggantikan blok post { always { ... } }
            junit 'target/surefire-reports/*.xml'
        }
    }

    stage('Deliver') {
        sh './jenkins/scripts/deliver.sh'
    }
}