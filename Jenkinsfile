node {
    
	

    env.AWS_ECR_LOGIN=true
    def newApp
    def registry = 'anubhav01jain/docker-test'
    def registryCredential = 'dockerhub'
	
	stage('Git') {
		git 'https://github.com/anubhav01jain/node-todo-frontend'
	}
	stage('Install dependencies') {
            nodejs('nodejs') {
                sh 'npm install'
                echo "Modules installed"
            }
	}
	
	stage('Test') {
            nodejs('nodejs') {
                sh 'npm test'
                echo "Modules tested"
            }
	}
	stage('Push image') {
        /* 
			You would need to first register with DockerHub before you can push images to your account
		*/
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
            } 
                echo "Trying to Push Docker Build to DockerHub"
    }
}
	

