pipeline {
    agent any

    stages {
        stage('Cloning project') {
            steps {
                git branch: 'main', url: 'https://github.com/irvieira/jk-public-gh.git'
            }
        }
        stage('Building image') {
            steps {
                sh 'docker build -t webapp:${BUILD_NUMBER} .'
            }
        }
        stage('Deploying') {
            steps {
                sh '''
                docker stop webapp_ctr
                docker run --rm -d -p 3000:3000 --name webapp_ctr webapp:${BUILD_NUMBER}
            '''
            }
        }
    }
}
