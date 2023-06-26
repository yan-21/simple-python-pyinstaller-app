node {
    stage('Build') {
        docker.image('python:2-alpine') {
            sh 'python -m py_compile sources/add2vals.py sources/calc.py'
        }
    }
    stage('Test') {
        docker.image('python:2-alpine') {
           sh 'py.test --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
        }
    }
}