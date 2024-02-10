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
		stage('Analisis estatico de codigo'){
			steps{
				sh 'make cppcheck-xml'
				recordIssues(tools: [cppCheck(pattern: 'reports/cppcheck/*.xml')])
			}
		}
	        stage('Tests unitarios') {
	            steps {
        	        sh 'make tests-xml'
               		junit stdioRetention: '', testResults: 'tests/cmocka/*.xml'
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
