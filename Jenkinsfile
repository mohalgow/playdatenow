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
	
        stage('Deploy') {
            steps {
                sh 'aws configure set region us-east-1	'
                sh 'aws elasticbeanstalk create-application-version --application-name $AWS_EB_APP_NAME --version-label $AWS_EB_APP_VERSION --source-bundle S3Bucket=$AWS_S3_BUCKET,S3Key=$ARTIFACT_NAME'
                sh 'aws elasticbeanstalk update-environment --application-name $AWS_EB_APP_NAME --environment-name $AWS_EB_ENVIRONMENT_NAME --version-label $AWS_EB_APP_VERSION'
            }
	}
    }
	post {
		always {
			sh 'docker logout'
		}
	}

}
