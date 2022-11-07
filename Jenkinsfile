pipeline {

    agent any

    environment {
        dockerhub_registry = "orendin8/devops_project"
        dockerhub_credential = 'dockerhub'
        dockerImage = ''
        github_credential = "9YvQFinxGdQNZXu8/pmb/G3H0CXrpWFK3D7tzq2sUZs"
        github_url = "https://github.com/OrenDin8/devopsProject"
	test_cerdentials = "jenkins-ec2-server-credentials"

    }
    stages {
        stage('Build Image') {
            steps {
                script {
                    dockerImage = docker.build dockerhub_registry + ":latest"
                }
            }
        }
	stage('Test') {
            steps {
                sshagent() {
                    sh """
                        echo 'Test stage ...'
                        bash -x deploy.sh test
                        """
                }
            }
        }
        stage('Push to dockerhub') {
            steps {
               script {
                    docker.withRegistry( '', dockerhub_credential) {
                        dockerImage.push()
                    }
                }
            }
        }
   
        stage ('Production') {
	    steps {
	    	sh """
                     echo 'Prodaction stage ...'
                     bash -x deploy.sh test
                   """
            }
        }
    }
 }
