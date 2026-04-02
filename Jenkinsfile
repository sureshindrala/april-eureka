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
    SONAR_HOST= 'http://34.57.207.225:9000'
    POM_VERSION = readMavenPom().getVersion()
    POM_PACKAGING = readMavenPom().getPackaging()    
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
        steps {
        echo "*******${env.APPLICATION_NAME}-sonar scaning*************"
         withCredentials([string(credentialsId: 'sonar_creds', variable: 'sonar_creds')])
            sh """
                mvn clean verify sonar:sonar \
                -Dsonar.projectKey=chathura-eureka \
                -Dsonar.host.url=$SONAR_HOST \
                -Dsonar.login=$sonar_creds        

            """
        }

    }
    stage('Build Format') {
        steps {
                echo "***************************Printing Build Format*****************************"
                script {
                    sh """
                    echo "Testing JAR SOURCE: chathura-${env.APPLICATION_NAME}-${env.POM_VERSION}.${env.POM_PACKAGING}"
                
                    """
                    // sh "cp ${workspace}/target/i27-${env.APPLICATION_NAME}-${env.POM_VERSION}.${env.POM_PACKAGING} ./.cicd"
                    // sh "ls -la ./.cicd"
                    // sh "docker build --force-rm --no-cache --pull --rm=true --build-arg JAR_SOURCE=i27-${env.APPLICATION_NAME}-${env.POM_VERSION}.${env.POM_PACKAGING} -t ${env.DOCKER_HUB}/${env.APPLICATION_NAME}:${GIT_COMMIT} ./.cicd "
                }
            }
    }    
    
 }

}