pipeline {
    agent {
        docker {
            image 'projectdiscovery/nuclei:latest'
            // The image's entrypoint is "nuclei", which breaks Jenkins' container handling.
            // HOME=/tmp gives Nuclei a writable place for its templates.
            args '--entrypoint= -e HOME=/tmp'
        }
    }
    environment {
        TARGET = 'https://scanme.sh'   // change to your own target
    }
    options {
        timeout(time: 30, unit: 'MINUTES')
    }
    stages {
        stage('Nuclei Scan') {
            steps {
                sh 'nuclei -version'
                sh 'nuclei -update-templates'
                sh 'nuclei -u "$TARGET" -severity low,medium,high,critical -nc'
            }
        }
    }
}
