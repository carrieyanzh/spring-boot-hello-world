pipeline {
    agent any

    environment {
  //      MAVEN_HOME = '/usr/share/maven' // Path to Maven installation
        SONARQUBE_SERVER = 'mySonarQube'  // SonarQube server configured in Jenkins
        NEXUS_REPO = 'http://nexus.example.com/repository/maven-releases/' // Nexus repository URL
    }

    tools {
        maven 'mymaven'
    }
    stages {
        stage('Checkout Code') { // Clones the repository
            steps {
               git branch: 'main', url: 'https://github.com/carrieyanzh/spring-boot-hello-world.git'
            }
        }
        stage('Build with Maven') { // Builds the project and creates JAR/WAR
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Build with test') { // Builds the project and creates JAR/WAR
            steps {
                sh 'mvn test'
            }
        }
         stage('Build with sonarqube') { // Builds the project and creates JAR/WAR
            steps {
                withSonarQubeEnv(SONARQUBE_SERVER){
                    sh 'mvn sonar:sonar'
                }
            }
        }
    }
    post {
        success {
            echo 'Build and deployment successful!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
