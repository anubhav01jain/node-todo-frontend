node {
    
	

    env.AWS_ECR_LOGIN=true
    def newApp
    def registry = 'anubhav01jain/docker-test'
    def registryCredential = 'dockerhub'
	
	stage('Git') {
		git 'https://github.com/anubhav01jain/node-todo-frontend'
	}
	stage('Build') {
            nodejs('nodejs') {
                sh 'npm run build'
                echo "Build completed"
            }
	}
	stage('Test') {
		sh 'npm test'
	}
	stage('Building image') {
        docker.withRegistry( 'https://' + registry, registryCredential ) {
		    def buildName = registry + ":$BUILD_NUMBER"
			newApp = docker.build buildName
			newApp.push()
        }
	}
	stage('Registring image') {
        docker.withRegistry( 'https://' + registry, registryCredential ) {
    		newApp.push 'latest2'
        }
	}
    stage('Removing image') {
        sh "docker rmi $registry:$BUILD_NUMBER"
        sh "docker rmi $registry:latest"
    }
    
}
