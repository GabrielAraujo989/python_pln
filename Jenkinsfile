pipeline {
    agent any

    stages {
        stage('Preparação do Ambiente') {
            steps {
                sh '''
                    # Atualizar pacotes e instalar Python3 e pip
                    apt-get update
                    apt-get install -y python3 python3-pip
                    
                    # Verificar a versão do Python instalado
                    python3 --version
                    pip3 --version
                    
                    # Instalar os requisitos do projeto
                    pip3 install -r requisitos.txt
                '''
            }
        }

        stage('Execução do Teste Levenshtein') {
            steps {
                sh 'python3 levenshtein_teste.py'
            }
        }

        stage('Verificação do Arquivo de Perguntas') {
            steps {
                script {
                    if (fileExists('perguntas.txt')) {
                        echo 'Arquivo perguntas.txt encontrado!'
                    } else {
                        error('Arquivo perguntas.txt não encontrado. Interrompendo o pipeline.')
                    }
                }
            }
        }

        stage('Execução do Chatbot') {
            steps {
                sh 'python3 chat_bot.py'
            }
        }
    }
}
