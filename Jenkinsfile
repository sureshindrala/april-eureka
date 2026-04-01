pipeline {
    agent {
        label 'k8s-slave'
    }
    tools {
        maven 'Maven-3.9.14'
        jdk 'JDK-17'
}
environment {
    APPLICATION_NAME = "eureka"
}
stages {
    stage(************build-stage************************) {
        steps {
           
            sh "mvn clean package -Dmaven.test.skip=true"
        }

    }
 }

}