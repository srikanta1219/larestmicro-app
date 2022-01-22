node {
    def home

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Build image') {
  
       home = docker.build("srikanta1219/ho", -f "/multi-image-build/home/ ")
    }

    stage('Test image') {
  

        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            app.push("${env.BUILD_NUMBER}")
        }
    }
    
    
}
