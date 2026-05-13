pipeline {
	agent any
	stages {
		stage('Descargar Código') {
			steps {
				echo 'Clonando el repositorio...'
				git branch: 'desarrollo', url:
'https://github.com/Chiquito921/proyecto-devsecops.git'
	}
	}
	stage('Construir Imagen (Build)') {
		steps {
			echo 'Construyendo el container...'
			sh 'docker build -t mi-app-segura:latest .'
			}
		}
	stage('Analisis de Seguridad Trivy'){
		steps {
			echo 'Buscando vulnerabilidades criticas...'
			// Ejecutamos Trivy en la plaza del pueblo

			sh 'docker run --rm -v /var/run/docker.sock:/var/run/docker.sock aquasec/trivy image --exit-code 1 --severity CRITICAL mi-app-segura:latest'
}
}
	stage('Despliegue en Produccion') {
		steps {
			echo 'Todo correcto y yo que me alegro'
			// Detenemos el contenedor viejo
			sh 'docker stop app-produccion || true'
			sh 'docker rm app-produccion || true'
			sh 'docker run -d -name app-produccion mi-app-segura:latest'
}
}
}
}