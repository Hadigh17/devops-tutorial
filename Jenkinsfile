node {
    def app

    stage('Clone repository') {
        // Clone repo into Jenkins workspace
        checkout scm
    }

    stage('Build image') {
        // Build Docker image
        app = docker.build("hadigh17/tutoriall")
    }

    stage('Test image') {
    steps {
        script {
            app.inside('--entrypoint ""') {  // run without mounting workspace
                sh 'echo Running inside container'
            }
        }
    }
}


    stage('Push image') {
        // Push image to Docker Hub
        docker.withRegistry('https://index.docker.io/v1/', 'docker-hub') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}
