pipeline {
	agent any

	environment {
		IMAGE_NAME = 'jenkins-docker-chali-cajbon'
		CONTAINER_NAME = 'jenkins-docker-web'
		HOST_PORT = '8181'
		CONTAINER_PORT = '80'
		IMAGE_TAG = "${BUILD_NUMBER}"
		FULL_IMAGE_NAME = "${IMAGE_NAME}:${BUILD_NUMBER}"
	}

	stages {
		stage('Clonación') {
			steps {
				checkout scm
			}
		}

		stage('Verificación') {
			steps {
				sh 'test -f index.html'
				sh 'test -f Dockerfile'
			}
		}

		stage('Construcción') {
			steps {
				sh 'docker build -t "$FULL_IMAGE_NAME" .'
			}
		}

		stage('Despliegue') {
			steps {
				sh '''
					if docker ps -a --format '{{.Names}}' | grep -qx "$CONTAINER_NAME"; then
					  docker rm -f "$CONTAINER_NAME"
					fi

					docker run -d --name "$CONTAINER_NAME" -p "$HOST_PORT:$CONTAINER_PORT" "$FULL_IMAGE_NAME"
				'''
			}
		}

		stage('Confirmación') {
			steps {
				echo "Proceso exitoso: la imagen ${FULL_IMAGE_NAME} fue construida y el contenedor ${CONTAINER_NAME} quedó en ejecución."
			}
		}
	}

	post {
		failure {
			echo 'Proceso fallido: revise la salida de consola de Jenkins para identificar el error.'
		}
		success {
			echo 'Pipeline completado correctamente.'
		}
	}
}
