node {
    stage('Git Checkout') {
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
        sh 'docker login -u rajesh1218 -p $PASSWORD'
    }
    stage("Push Image to Docker Hub"){
        sh 'docker push rajesh1218/rja-boot-app:latest'
    }
    stage("SSH Into k8s Server") {
        def remote = [:]
        remote.name = 'K8S master'
        remote.host = '192.168.56.111'
        remote.user = 'vagrant'
        remote.password = 'vagrant'
        remote.allowAnyHosts = true
        
        stage('Put k8s-spring-boot-deployment.yml onto k8smaster') {
            sshPut remote: remote, from: 'k8s-spring-boot-deployment.yml', into: '.'
        }
        stage('Deploy spring boot') {
          sshCommand remote: remote, command: "kubectl apply -f k8s-spring-boot-deployment.yml"
        }
    }
}
