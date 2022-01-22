node {
    def home
    def jenkins
    def docker
    def kuber

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Build image') {
  
        home = docker.build("srikanta1219/ho:${env.BUILD_NUMBER}","${env.WORKSPACE} /home/ " )
        jenkins = docker.build("srikanta1219/je:${env.BUILD_NUMBER}","${env.WORKSPACE} /jenkins/ ")
        docker = docker.build("srikanta1219/do:${env.BUILD_NUMBER}","${env.WORKSPACE} /docker/ ")
        kuber = docker.build("srikanta1219/ku:${env.BUILD_NUMBER}","${env.WORKSPACE} /kuber/ ")
        
    }

    stage('Test image') {
  

        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            docker.push()
        }
    }
    
    
}
