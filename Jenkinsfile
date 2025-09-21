node {
    def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

        app = docker.build("hadigh17/tutoriall")
    }

    stage('Test image') {
        /* Ideally, we would run a test framework against our image.
         * For this example, we're using a Volkswagen-type approach ;-) */

        steps {
        script {
            docker.image('hadigh17/tutoriall').inside('-w /c/Users/hadig/.jenkins/workspace/edureka-pipeline/') {
                sh 'echo Running inside container'
            }
        }
        }
    }

    stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
        docker.withRegistry('https://hub.docker.com/repositories/hadigh17', 'docker-hub') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}
