pipeline { 
    agent any 
    stages {
        stage('Git-CheckOut') { 
            steps { 
                //sh 'make'
                echo "checking out from git repo"
                git 'https://github.com/cchen1988/jenkins_pipeline.git'
            }
        }
        stage('Build'){
            steps {
                //sh 'make check'
                //junit 'reports/**/*.xml'
                echo "building image from repo"
                sh "docker build -t jenkins ."
            }
        }
        steps("Push to ECR") {
            withAWS(credentials: 'aws', region: 'us-east-1') {
                sh "docker tag jenkins:latest 556524976393.dkr.ecr.us-east-1.amazonaws.com/jenkins:latest"
                sh "docker push 556524976393.dkr.ecr.us-east-1.amazonaws.com/jenkins:latest"
              }
        }
    }
}

