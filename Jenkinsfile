pipeline {
    agent any

    stages {
        stage('Clonar Repositório') {
            steps {
                script {
                    // Clonar o repositório
                    git branch: 'main', url: 'https://github.com/GlhermePereira/git-tag-docker.git'
                }
            }
        }

        stage('Verificar Tag') {
            when {
                // Verifica se o commit foi feito por uma tag
                expression { return env.GIT_COMMIT ==~ /refs\/tags\// }
            }
            steps {
                script {
                    echo "Pipeline rodando com a tag: ${env.GIT_TAG}"
                }
            }
        }

        stage('Build Normal') {
            when {
                not {
                    // Executa apenas quando não é uma tag
                    expression { return env.GIT_COMMIT ==~ /refs\/tags\// }
                }
            }
            steps {
                echo 'Build normal (sem tag).'
            }
        }
    }
    post {
        always {
            echo 'Pipeline finalizado.'
        }
    }
}

