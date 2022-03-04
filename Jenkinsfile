pipeline { 
    agent any
     stages { 
        stage('build') { 
            steps { sh './gradlew clean build' } 
        } 
        stage('upload') { 
            steps { 
                sh 'aws s3 cp build/libs/application.war s3://final-jenkins-springboot-ys/application.war --region us-east-1' 
            }
        } 
        stage('deploy') { 
            steps { 
                 sh 'aws elasticbeanstalk create-application-version --region us-east-1 --application-name final-jenkins-springboot --version-label ${BUILD_TAG} --source-bundle S3Bucket="final-jenkins-springboot-ys",S3Key="application.war"' 
                 sh 'aws elasticbeanstalk update-environment --region us-east-1 --environment-name Finaljenkinsspringboot-env --version-label ${BUILD_TAG}' 
            } 
        } 
    } 
}