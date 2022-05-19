pipeline{

	agent any

	environment {
		// DOCKERHUB_CREDENTIALS=credentials('DockerHub')
		// KUBECONFIG="/etc/rancher/rke2/rke3.yaml"
		TAG = "latest"
	}

	stages {

		stage('Skip Build') {
                steps {
					script{
						def result = sh (script: "git log -1 | grep '\\[ci skip\\]'", returnStatus: true) 
						if (result != 0) {
						echo "performing build..."
						} else {
							currentBuild.result = 'ABORTED'
							error('Stopping early…')
						}
					}
                    
                }
            }
		stage('Deploy the image in kubernetes cluster') {
			steps{
				script{
					withKubeConfig([credentialsId: 'Kubernetes', serverUrl: 'https://192.168.49.2:8443']) {
      				sh 'kubectl apply -f ./cluster/flask-deployment.yaml'
					sh 'kubectl apply -f ./cluster/flask-service.yaml'
					sh 'kubectl apply -f ./cluster/redis-deployment.yaml'
					sh 'kubectl apply -f ./cluster/redis-service.yaml'

    		}

			}
			}
		}
		
	}

}