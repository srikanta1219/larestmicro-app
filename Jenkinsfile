node {
    def home
    def jenkins
    def docker
    def kuber

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Build image') {
  
       home = docker.build ("srikanta1219/ho",  "${env.WORKSPACE}/home/ ")
       jenkins = docker.build ("srikanta1219/jen",  "${env.WORKSPACE}/jenkins/ ")
       docker = docker.build ("srikanta1219/dock",  "${env.WORKSPACE}/docker/ ")
       kuber = docker.build ("srikanta1219/kube",  "${env.WORKSPACE}/kuber/ ")
       
    }

    stage('Test image') {
  

        home.inside {
            sh 'echo "Tests passed"'
        }
        jenkins.inside {
            sh 'echo "Tests passed"'
        }
        docker.inside {
            sh 'echo "Tests passed"'
        }
        kuber.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            home.push("${env.BUILD_NUMBER}")
            jenkins.push("${env.BUILD_NUMBER}")
            docker.push("${env.BUILD_NUMBER}")
            kuber.push("${env.BUILD_NUMBER}")
        }
    }
    
    
}
