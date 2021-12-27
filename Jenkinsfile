pipeline {
    agent { 
	docker { image 'python:3.9' } 
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
                sh 'printenv'
                sh 'python3 --version'
		sh 'python3 -m pip install -r requirements.txt'
		sh 'python3 setup.py install'
            }
        }
        stage('tests'){
            steps{
		sh 'pytest -v tests'
            }    
        }
    }
}
