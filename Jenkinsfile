pipeline {

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('docker-token')
		AWS_ACCESS_KEY_ID     = credentials('Access_key_ID')
  		AWS_SECRET_ACCESS_KEY = credentials('Secret_access_key')
		ARTIFACT_NAME = 'playdatenow_v03b-0.0.1-SNAPSHOT.war'
		AWS_S3_BUCKET = 'playdate-s3'
		AWS_EB_APP_NAME = 'playdate'
        AWS_EB_ENVIRONMENT_NAME = 'Playdate-env'
        AWS_EB_APP_VERSION = "${BUILD_ID}"
	}

	stages {
        stage('Build') {
            steps {
                sh 'echo "Building"'
                sh 'echo $AWS_ACCESS_KEY_ID'
                sh 'echo $AWS_SECRET_ACCESS_KEY'
            }
        }
        stage('Test') {
            steps {
                sh 'echo "Testing"'
            }
        }
        stage('Publish') {
            steps {
                sh 'echo "Publishing"'
            }
            post {
                success {
                    sh 'echo "Deploying to EB"'
                    sh 'sudo chmod 775 ./deploy_app.sh'
                    sh './deploy_app.sh'
                }
            }
        }
    }
}
