pipeline {
    agent any
    environment {
        AWS_ACCESS_KEY_ID = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
        AWS_DEFAULT_REGION = "us-east-1"
    }

    stages {
        stage('Terraform Cloud') {
            steps {
                script {
                    def terraformToken = 'MNy1zgG9zWzSmw.atlasv1.zauXBae5FaZ41jV3bZRXcyjeY1LhnPifqEbUpEMblP8dTq6yksbzemVJ08RaRswOA7M'
                    def workspaceName = 'jenkins_terraform'
                    def organizationName = 'cloudprof'

                    def requestBody = """
                    {
                        "data": {
                            "attributes": {
                                "is-destroy": false
                            },
                            "type": "runs"
                        }
                    }
                    """

                    def response = sh(script: """
                        curl -X POST "https://app.terraform.io/api/v2/organizations/${organizationName}/workspaces/${workspaceName}/runs" \\
                        -H "Authorization: Bearer ${terraformToken}" \\
                        -H "Content-Type: application/vnd.api+json" \\
                        -d '${requestBody}'
                    """, returnStatus: true)

                    if (response == 0) {
                        echo "Terraform run triggered successfully."
                    } else {
                        error "Failed to trigger Terraform run."
                    }
                }
            }
        }
    
        stage("run terraform") {
            steps {
                script {
                    dir('terraform') {
                        sh "terraform init"
                        sh "terraform apply -auto-approve"
                    }
                }
            }
        }
    }
}
