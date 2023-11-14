pipeline {
    agent any
    stage('Build') {
       steps {
           sh '''
                aws ecr-public get-login-password --region us-east-1 | docker login --username AWS --password-stdin public.ecr.aws/q1f8b0h6
                docker build -t roberta-amin .
                docker tag roberta-amin:latest public.ecr.aws/q1f8b0h6/roberta-amin:latest
                docker push public.ecr.aws/q1f8b0h6/roberta-amin:latest
           '''
       }
    }
}