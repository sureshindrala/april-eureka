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
    stage('************build-stage************************') {
        steps {

            echo "*****Building-${env.APPLICATION_NAME}******************"           
           sh "mvn clean package -DskipTests=true"
           // sh "mvn clean package -Dmaven.test.skip=true"
            archive 'target/*.jar'
        }

    }
    stage('***********************sonar-stage*******************'){
        echo "*******${env.APPLICATION_NAME}-sonar scaning*************"
        sh """
            mvn clean verify sonar:sonar \
            -Dsonar.projectKey=chathura-eureka \
            -Dsonar.host.url=http://34.57.207.225:9000 \
            -Dsonar.login=sqa_7b7618e38bb127784fc9b708e8890b0e551fafa5        

        """
    }
 }

}