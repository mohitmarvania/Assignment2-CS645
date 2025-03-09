pipeline {
	agent any 
	stages {
		stage("Building student survey application image") {
			steps {
				script {
					checkout scm
					sh 'echo ${BUILD_TIMESTAMP}'
					sh "docker login -u amisha1407 -p 123ami456A@" 
					def customImage = docker.build("amisha1407/amishafinalnew:${BUILD_TIMESTAMP}")
				}
			}
		}
		stage("Pushing Image to DockerHub") {
			steps {
				script {
					sh 'docker push amisha1407/amishafinalnew:${BUILD_TIMESTAMP}'
				}
			}
		}
		stage("Deploying to Rancher") {
			steps {
				script {
					sh 'kubectl set image deployment/assign2-deployment container-0=amisha1407/amishafinalnew:${BUILD_TIMESTAMP} -n default'
				}
			}
		}
	}
}
