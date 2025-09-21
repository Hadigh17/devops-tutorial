node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Build image') {
        app = docker.build("hadigh17/tutoriall")
    }

    stage('Test image') {
        // Replace app.inside with a plain docker run to avoid C:/ path issue
        bat 'docker run --rm hadigh17/tutoriall echo "Tests passed"'
    }

    stage('Push image') {
        docker.withRegistry('https://index.docker.io/v1/', 'docker-hub') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}
