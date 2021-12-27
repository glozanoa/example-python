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
		sh "python3 -m venv ${WORKSPACE}/env"
		withPythonEnv("${WORKSPACE}/env/bin/python3"){	
                	sh 'printenv'
                	sh 'python3 --version'
			sh 'python3 -m pip install --user -r requirements.txt'
			sh 'python3 setup.py install --user'
		}
            }
        }
        stage('tests'){
            steps{
		withPythonEnv("{WORKSPACE}/env/bin/python3"){
			sh 'pytest -v tests'
		}
            }    
        }
    }
}
