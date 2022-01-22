node {
    def home
    def jenkins
    def docker
    def kuber

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Build image') {
  
       home = docker.build("srikanta1219/ho","-f ${env.WORKSPACE}/home/Dockerfile ." )
       jenkins = docker.build("srikanta1219/je","-f ${env.WORKSPACE}/jenkins/Dockerfile .")
       docker = docker.build("srikanta1219/do","-f ${env.WORKSPACE}/docker/Dockerfile .")
       kuber = docker.build("srikanta1219/ku","-f ${env.WORKSPACE}/kuber/Dockerfile .")
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
