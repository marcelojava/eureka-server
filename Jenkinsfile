node {

   stage('Clone Repository') {
        // Get some code from a GitHub repository
        git 'https://github.com/marcelojava/eureka-server.git'

   }
   stage('Build Maven Image') {
        docker.build("maven-build")
         }

   stage('Run Maven Container') {

        //Remove eureka-server-container if it exisits
        sh "docker rm -f eureka-server-container"

        //Run maven image
        sh "docker run --rm --name eureka-server-container maven-build"
   }

   stage('Deploy Spring Boot Application') {

         //Remove eureka-server-container if it exisits
        sh " docker rm -f eureka-server-deploy-container"

        sh "docker run --name eureka-server-deploy-container --volumes-from eureka-server-container -d -p 8761:8761 cordis/eureka-server-deploy"
   }

}