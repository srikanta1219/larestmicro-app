node {
    def home
    def jenkins
    def docker
    def kuber

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Build image') {
  
       home = docker.build("srikanta1219/ho")
       jenkins = docker.build("srikanta1219/je")
       docker = docker.build("srikanta1219/do")
       kuber = docker.build("srikanta1219/ku")
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
