pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'python3.9 -m py_compile sources/add2vals.py sources/calc.py'
                stash(name: 'compiled-results', includes: 'sources/*.py*')
            }
        }
        stage('Test') {
            steps {
                sh 'python3.9 -m pip install pytest'
                sh 'python3.9 -m pytest --junit-xml test-reports/results.xml sources/test_calc.py'
            }
            post {
                always {
                    junit 'test-reports/results.xml'
                }
            }
        }

    }
}