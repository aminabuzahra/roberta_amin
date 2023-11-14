pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    // Fetch AWS ECR Public login token
                    def ecrLoginCommand = """
                        aws ecr-public get-login-password --region us-east-1
                    """
                    def ecrToken = sh(script: ecrLoginCommand, returnStdout: true).trim()

                    // Docker login to ECR Public
                    def dockerLoginCommand = """
                        docker login --username AWS --password-stdin public.ecr.aws/q1f8b0h6
                    """
                    sh(script: "${dockerLoginCommand} <<< '${ecrToken}'", returnStatus: true)

                    // Build and push Docker image
                    sh '''
                        docker build -t roberta-amin .
                        docker tag roberta-amin:latest public.ecr.aws/q1f8b0h6/roberta-amin:latest
                        docker push public.ecr.aws/q1f8b0h6/roberta-amin:latest
                    '''
                }
            }
        }
    }
}
