node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Build image') {

        app = docker.build("aboubakr/node")
    }

     stage('Test image') {
        app.inside {
            sh 'curl http://localhost:8000 || exit 1'
        }
    }   

    stage('Push image') {
       
     
   docker.withRegistry("https://registry.hub.docker.com", 'docker-hub-credential') {

            app.push("${env.BUILD_NUMBER}")
	    
            
        }
    }
}
