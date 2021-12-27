pipeline {
    agent { 
	docker { image 'python:3.9' } 
    }

    triggers {
        githubPush()
    }
    
    environment {
        DISABLE_AUTH = 'true'
        DB_ENGINE    = 'sqlite'
    }
    
    stages {
        stage('build') {
            steps {
                echo "Database engine is ${DB_ENGINE}"
                echo "DISABLE_AUTH is ${DISABLE_AUTH}"
		withPythonEnv('Python3'){	
                	sh 'printenv'
			sh 'whereis python3'
                	sh 'python3 --version'
			sh 'pip install -r requirements.txt'
			sh 'python3 setup.py install'
		}
            }
        }
        stage('tests'){
            steps{
		withPythonEnv('Python3'){
			sh 'pytest -v tests'
		}
            }    
        }
    }
}
