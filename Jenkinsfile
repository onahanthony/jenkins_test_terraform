pipeline {
    agent any
    environment {
        AWS_ACCESS_KEY_ID = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
        AWS_DEFAULT_REGION = "us-east-1
    }
    stages {
        stage("run terraform") {
            steps {
                script {
                    dir('terraform') {
                        sh "terraform init"
			sh "terraform plan"
                        sh "terraform apply -auto-approve"
                    }
                }
            }
        }
}
