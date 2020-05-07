node {
    def app

    stage('Clone repp') {
        /* Cloning the Repository to our Workspace */

        checkout scm
    }
    
    stage('Build Executable Jar'){
        steps {
             sh 'mvn clean test package'
        }
    }

    stage('Build image') {
        /* This builds the actual image */

        app = docker.build("vamceep99/calculator")
    }

    /*stage('Test image') {
        
        app.inside {
            echo "Tests passed"
        }
    }*/

    stage('Push image') {
        /* 
			You would need to first register with DockerHub before you can push images to your account
		*/
        docker.withRegistry('https://registry.hub.docker.com', 'docker_hub') {
        	echo "${env.BUILD_NUMBER}"
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
            } 
                echo "Trying to Push Docker Build to DockerHub"
    }
}