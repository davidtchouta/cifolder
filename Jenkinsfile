pipeline {
    agent any

    environment {
        // Ajoutez ici le chemin vers l'installation de conda, par exemple :
        // Pour une installation Anaconda
        CONDA_HOME = "C:\\Users\\dvid\\anaconda3"
        PATH = "${CONDA_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/davidtchouta/cifolder.git'
            }
        }

        stage('Setup Conda Environment') {
            steps {
                sh 'conda --version'
                sh 'conda create -n myenv python=3.9 -y'
                sh 'echo "source activate myenv" > activate_myenv.sh'
                sh '. activate_myenv.sh && conda install -y --file requirements.txt' // Installer les dépendances depuis un fichier requirements.txt
            }
        }

        stage('Run Tests') {
            steps {
                sh '. activate_myenv.sh && pytest'
            }
        }
    }

    post {
        always {
            junit '**/test-results.xml'
        }
    }
}

