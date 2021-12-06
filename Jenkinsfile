pipeline {
    agent any
    tools {
        maven "maven"
    }
    
    
    stages {
        stage('Build') { 
            steps {
                echo 'Building..'
                sh 'mvn -f pom.xml clean package' 
            }
        }
        stage('SonarCube-test') {
            steps {
                 sh '''export SONAR_TOKEN="9f3103312f3b2b3697205ce0b215abaaa1ddd106"
                 mvn verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar -Dsonar.projectKey=module6'''
            }
        }
            stage('docker build') {
                 steps {
        sh 'docker build -t hww-shalom:${BUILD_NUMBER} .'
      }
    }
      stage('docker tag') {
         steps {
        sh 'docker tag hww-shalom:${BUILD_NUMBER} localhost:8123/hww-shalom:${BUILD_NUMBER}'
      }
    }
        stage('docker push') {
             steps {
                script {
                  docker.withRegistry('http://localhost:8123', 'nexus') {
                      docker.build('hww-shalom').push(${BUILD_NUMBER}) }
        
      }
    }
}
      }
    
  environment {
    registry = 'localhost:8123/'
    imageName = 'hww-shalom'
    registryCredentials = 'nexus'
    buildId = ''
  }
}

