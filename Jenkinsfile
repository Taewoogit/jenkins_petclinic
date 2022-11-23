pipeline {
    agent  {
        label 'dind-agent'
    }
    stages {
        stage("Build") {
            steps {
                script {
                    sh "./mvnw clean install"
                }
            }
        }
        stage("Build image") {
            steps {
                script {
                    app = docker.build("midyear-spot-368821/petclinic")
                }
            }
          }
        stage('Push to registry') {
            steps {
             script {
                        docker.withRegistry('https://asia.gcr.io', 'gcr:midyear-spot-368821') {
                        app.push("${env.BUILD_NUMBER}")
                    }
                }
           }        
      }
   }
}
