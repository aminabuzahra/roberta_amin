pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    sh '''
                        aws ecr get-login-password --region eu-north-1 | docker login --username AWS --password-stdin 933060838752.dkr.ecr.eu-north-1.amazonaws.com
                        docker build -t amin-roberta .
                        docker tag amin-roberta:latest 933060838752.dkr.ecr.eu-north-1.amazonaws.com/amin-roberta:latest
                        docker push 933060838752.dkr.ecr.eu-north-1.amazonaws.com/amin-roberta:latest
                    '''
                }
            }
        }
    }
}