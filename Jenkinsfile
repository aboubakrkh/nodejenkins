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
	    sh 'docker run -it -p 8000:8000 aboubakr/node'
            sh 'curl http://127.0.0.1:8000 || exit 1'
        }
    }   

    stage('Push image') {
       
     
   docker.withRegistry("https://registry.hub.docker.com", 'docker-hub-credential') {

            app.push("${env.BUILD_NUMBER}")
	    
            
        }
    }
}
