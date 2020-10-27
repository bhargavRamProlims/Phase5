node {
	def application = "phase5_sportyshoe"
	def dockerhubaccountid = "bhargavasdramus"
	stages{
	stage('Clone repository') {
		checkout scm
	}

	stage('Build image') {
		app = docker.build("${dockerhubaccountid}/${application}:${BUILD_NUMBER}")
	}

	stage('Push image') {
		app.push()
		app.push("latest")
	}

	stage('Deploy') {
		sh ("docker run -d -p 3000:3000 ${dockerhubaccountid}/${application}:${BUILD_NUMBER}")
	}
	
	stage('Remove old images') {
		sh("docker rmi ${dockerhubaccountid}/${application}:latest -f")
   }
	}
}