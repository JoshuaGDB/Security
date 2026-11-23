pipeline {
    agent {
        docker {
            image 'projectdiscovery/nuclei:latest'
            
            args '--entrypoint= -e HOME=/tmp'
        }
    }
    environment {
        TARGET = 'https://scanme.sh' 
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
