pipeline {
  agent any    
  stages { 
    stage('Initialize'){
       steps {
         script {
           def dockerHome = tool 'docker'
           env.PATH = "${dockerHome}/bin:${env.PATH}"
        } 
      }
    }
    stage("Master") {
      when {
        branch 'master'
	 }
      steps {
        script {
        withCredentials([usernamePassword(credentialsId: "DOCKERHUB_TOKEN", usernameVariable: 'USERNAME', passwordVariable: 'TOKEN')]) {
            sh "docker login -u kiranbandana -p $TOKEN https://registry.hub.docker.com"
        }
         dockerImage = docker.build("kiranbandana/to-do:prod")    
         dockerImage.push()
        }
    }
    }
    stage("Develop") {
      when {
        branch 'develop'
	 }
      steps {
        script {
        withCredentials([usernamePassword(credentialsId: "DOCKERHUB_TOKEN", usernameVariable: 'USERNAME', passwordVariable: 'TOKEN')]) {
            sh "docker login -u kiranbandana -p $TOKEN https://registry.hub.docker.com"
        }
         dockerImage = docker.build("kiranbandana/to-do:staging")    
         dockerImage.push()
        }
    }
    }
}
}


