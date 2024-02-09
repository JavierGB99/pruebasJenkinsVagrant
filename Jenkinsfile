pipeline{
	agent any
	stages{
		stage('Obtener el repositorio'){
			steps{
				git branch: 'main', url: 'https://github.com/JavierGB99/pruebasJenkinsVagrant.git'
			}
		}
		stage('Generar la documentacion') {
			steps{
				sh "doxygen"
			}
		}
	}
	post {
        	success {
            		publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: 'html/', reportFiles: 'html/', reportName: 'Documentación', reportTitles: ''])
            		archive "documentation.zip"
        	}
    	}
}
