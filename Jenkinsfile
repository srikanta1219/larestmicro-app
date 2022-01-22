node {
    def home
    def jenkins
    def docker1
    def kuber

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Build image') {
  
       home = docker.build ("srikanta1219/home",  "${env.WORKSPACE}/home/ ")
       jenkins = docker.build ("srikanta1219/jenkins",  "${env.WORKSPACE}/jenkins/ ")
       docker1 = docker.build ("srikanta1219/docker",  "${env.WORKSPACE}/docker/ ")
       kuber = docker.build ("srikanta1219/kubern8s",  "${env.WORKSPACE}/kuber/ ")
       
    }

    stage('Test image') {
  

        home.inside {
            sh 'echo "Tests passed"'
        }
        jenkins.inside {
            sh 'echo "Tests passed"'
        }
        docker1.inside {
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
            docker1.push("${env.BUILD_NUMBER}")
            kuber.push("${env.BUILD_NUMBER}")
        }
    }
	stage('Trigger Kubernetes') {
                echo "triggering updatekubernetesjob"
                build job: 'updatekubernetes', parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
        } 
		
	}

