pipeline{
    agent any

    stages {

        stage('Despliegue QA Notificacion'){
            steps{
                echo 'Desplegando en QA Notificacion '
            }
        }
        stage('Aprobacion manual'){
            input {
                message "Esta seguro que desea desplegar a produccion?"
                ok "Aprobar"
                parameters {
                    string(name: 'comentario', defaultValue: '', description: 'Deje aqui')
                }
            }

            steps {
                echo "${comentario}"
            }
        }

        stage('Despliegue PROD Notificacion...'){
            steps {
                echo "Desplegando en produccion Notifi"
                sh "./mvnw package -Pprod verify -DskipTest jib:dockerBuild"
                sh "docker-compose -f ./src/main/docker/app.yml up -d --build"
            }
        }
    }
}
