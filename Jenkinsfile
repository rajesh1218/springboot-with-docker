node {
    stage('Build') {
        git 'https://github.com/rajesh1218/springboot-with-docker.git'
    }
    stage('Gradle Build') {
       sh './gradlew build'
    }
    stage("Docker build"){
        sh 'docker version'
        sh 'docker build -t jhooq-docker-demo .'
        sh 'docker image list'
        sh 'docker tag rja-boot-app rajesh1218/rja-boot-app:latest'
    }
}
