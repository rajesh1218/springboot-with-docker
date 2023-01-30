node {
    stage('Build') {
        git 'https://github.com/rajesh1218/springboot-with-docker.git'
    }
    stage('Gradle Build') {
       sh './gradlew build'
    }
    stage("Docker build"){
        sh 'docker version'
        sh 'docker build -t rja-boot-app .'
        sh 'docker image list'
        sh 'docker tag rja-boot-app rajesh1218/rja-boot-app:latest'
    }
    withCredentials([string(credentialsId: 'DOCKER_HUB_PASSWORD', variable: 'PASSWORD')]) {
        sh 'docker login -u rajesh1218 -p $PASSWORD
    }
    stage("Push Image to Docker Hub"){
        sh 'docker push rajesh1218/rja-boot-app:latest'
    }
}
