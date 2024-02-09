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
		stage('Archivar documentacion'){
			steps{
				sh "zip documentation.zip -r html/*"
			}
		}
	}
	post {
        	success {
            		publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: 'html/', reportFiles: 'files.html', reportName: 'Documentación', reportTitles: ''])
            		archive "documentation.zip"
        	}
    	}
}
