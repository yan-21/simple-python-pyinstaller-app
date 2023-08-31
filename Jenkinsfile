node {
    stage('Build') {
        docker.image('python:2-alpine').inside {
            checkout scm
            sh 'python -m py_compile sources/add2vals.py sources/calc.py'
        }
    }
    stage('Test') {
        docker.image('qnib/pytest').inside {
            checkout scm
            sh 'py.test --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
            junit 'test-reports/results.xml'
        }
    }
    stage('Deliver') {
        agent {
            docker {
                image 'cdrx/pyinstaller-linux:python2'
            }
        }
        steps {
            script {
                sh 'pyinstaller --onefile sources/add2vals.py'
            }
        }
        post {
            success {
                archiveArtifacts 'dist/add2vals'
            }
        }
    }
}
