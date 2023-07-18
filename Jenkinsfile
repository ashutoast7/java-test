pipeline {
    agent any

    environment {
        function_name = 'java-sample'
    }
   

    stages {
        stage('Build') {
            steps {
                echo 'Build'
                sh 'mvn package'
            }
        }

        stage('Push') {
            steps {
                echo 'Push'

                sh "aws s3 cp target/sample-1.0.3.jar s3://sonarbucket-toast"
            }
        }

        stage('Deploy') {
            steps {
                echo 'Build'

                sh "aws lambda update-function-code --function-name $function_name --region us-east-2 --s3-bucket sonarbucket-toast --s3-key sample-1.0.3.jar"
            }
        }
    }
}
