node {
    stage('Build') {
        git 'https://github.com/rajesh1218/springboot-with-docker.git'
    }
    stage('Gradle Build') {
       sh './gradlew build'
    }
}
