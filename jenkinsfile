pipeline {
    agent any

    stages {
        stage('Test') {
            steps {
                echo 'Testing started'
                sh 'test -f test.html'
                sh 'grep -q "<html>" test.html'
                echo 'Testing passed'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploy started'

                sh '''
                scp -o StrictHostKeyChecking=no test.html ubuntu@172.31.45.246:/tmp/
                scp -o StrictHostKeyChecking=no test.html ubuntu@172.31.35.65:/tmp/

                ssh -o StrictHostKeyChecking=no ubuntu@172.31.45.246 "sudo cp /tmp/test.html /var/www/html/index.html"
                ssh -o StrictHostKeyChecking=no ubuntu@172.31.35.65 "sudo cp /tmp/test.html /var/www/html/index.html"
                '''

                echo 'Deployment completed'
            }
        }
    }
}
