node {
    def home
    def jenkins
    def docker
    def kuber

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Build image') {
  
       home = docker.build("srikanta1219/ho","-f /home/Dockerfile ." )
       jenkins = docker.build("srikanta1219/je","-f /jenkins/Dockerfile .")
       docker = docker.build("srikanta1219/do","-f /docker/Dockerfile .")
       kuber = docker.build("srikanta1219/ku","-f /kuber/Dockerfile .")
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
