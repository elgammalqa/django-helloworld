#!/usr/bin/env groovy

pipeline {
  
	agent { label 'master' }

	stages {
        stage ('Checkout') {
			steps{
        	git clone "https://github.com/elgammalqa/django-helloworld.git"
        }
	}
		stage ('Docker Build and Docker Push') {
		    steps{
              script {
                sh "docker log -u amirelgammal -p *******"
              }
            }
			steps{
			    sh "pwd"
				sh "ansible-playbook ansible/docker_build.yml"
			}	
        }
		stage ('Test latest build') {
		    steps{
              script {
                sh "echo 'Testing newly build image'"
              }
            }
        }
		stage ('Docker tag as latest') {
		    steps{
              script {
				sh "ansible-playbook ansible/docker_latest_tag.yml"
              }
            }
        }

      	stage ('Kubernetes Deploy') {
			  steps{
            	sh "ansible-playbook ansible/main.yml"
			  }
      	} 
	}
}