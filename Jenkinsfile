pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM',
                branches: [[name: '*/main']],
                extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'my-project']],
                userRemoteConfigs: [[url: 'https://github.com/cd-hgupta/Jenkins_s3.git']]])
            }
        }
        stage('Zip Files') {
            steps {
                sh 'cd my-project && zip -r ../my-project.zip *'
            }
        }
        stage('Upload to S3') {
            steps {

                dir('/var/lib/jenkins/workspace/Jenkin_s3') {

                    pwd(); //Log current directory

                    withAWS(region:'us-east-1',credentials:'') {

                        

                        // Upload files from working directory 'dist' in your project workspace
                        s3Upload(bucket:"jenu", workingDir:'', includePathPattern:'**/*');
                    }
                }

            };
        }
    }
}
