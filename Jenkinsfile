node {
    def app

    stage('Clone repository') {
        /* Cloning the Repository to our Workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image */
	sh "docker build -t pavan323/app:latest ."
        /*sh "docker build -t pavan323/app:${currentBuild.number} ."
        app = docker.build("pavan323/nodeapp")*/
    }


    stage('Push image') {
        /* 
			You would need to first register with DockerHub before you can push images to your account
		*/
        /*docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
            }*/
        withCredentials([string(credentialsId: 'DockerUsername', variable: 'DockerUsername'), string(credentialsId: 'DockerPassword', variable: 'DockerPassword')]) {
		    sh "docker login -u pavan323 -p ${DockerPassword}"
		    sh "docker push pavan323/app"
	}
                echo "Trying to Push Docker Build to DockerHub"
    }
    stage('Kubernets Deployment') {
        /* 
			You would need to first register with DockerHub before you can push images to your account
		*/
        sh "kubectl apply -f flasktestapp.yaml"
	sh "kubectl get services"
	echo "Hello World"
    }

}
