node {
    stage('Cleanup') {
        step([$class: 'WsCleanup'])
    }
    stage('Checkout SCM') {
        checkout scm
        echo "code checkout done"
    }
    def pythonImage
    stage('build docker image') {
        pythonImage = docker.build("jalajsahni/edureka")
    }
    stage('test') {
        pythonImage.inside {
            sh '. /tmp/venv/bin/activate && python -m pytest --junitxml=build/results.xml'
        }
    }
    stage('collect test results') {
        junit 'build/results.xml'
    }
}
