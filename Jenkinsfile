node {
    def home
    def jenkins
    def docker
    def kuber

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Build image') {
  
        sh  'home = docker.build("srikanta1219/ho","-f ${env.WORKSPACE}/home/Dockerfile ." )'
        sh  'jenkins = docker.build("srikanta1219/je","-f ${env.WORKSPACE}/jenkins/Dockerfile .")'
        sh  'docker = docker.build("srikanta1219/do","-f ${env.WORKSPACE}/docker/Dockerfile .")'
        sh  'kuber = docker.build("srikanta1219/ku","-f ${env.WORKSPACE}/kuber/Dockerfile .")'
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
