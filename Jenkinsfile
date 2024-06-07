pipeline {
    agent any
    tools {
        conda 'Anaconda3' // Utiliser l'installation Conda configurée
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/davidtchouta/cifolder.git'
            }
        }

        stage('Setup Conda Environment') {
            steps {
                script {
                    // Initialiser conda
                    def condaHome = tool name: 'Anaconda3', type: 'Conda'
                    env.PATH = "${condaHome}/bin:${env.PATH}"
                }
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
