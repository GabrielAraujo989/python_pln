pipeline {
    agent any

    parameters {
        string(name: 'DIGITE_A_PERGUNTA', defaultValue: '', description: 'Faça a pergunta')
    }

    stages {
        stage('Preparação do Ambiente') {
            steps {
                echo 'Já instalado'
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
                script {
                    def pergunta = params.DIGITE_A_PERGUNTA
                    sh "python3 chat_bot.py '${pergunta}'"
                }
            }
        }
    }
}
