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
        sh ''
        'export SONAR_TOKEN="9f3103312f3b2b3697205ce0b215abaaa1ddd106"
        mvn verify org.sonarsource.scanner.maven: sonar - maven - plugin: sonar - Dsonar.projectKey = module6 ''
        '
      }
    }
    stage('docker build') {
      steps {
        sh 'docker build -t hww-shalom:latest .'
      }
    }
  }
  stage('docker tag') {
    steps {
      sh 'docker tag hello_world_war:latest 192.168.1.224:8123/hello_world_war:latest'
    }
  }
  stage('docker push') {
    steps {
      script {
        docker.withRegistry('http://localhost:8123', 'nexus') {
          docker.build('hello_world_war').push('latest')
        }

      }
    }
  }
  environment {
    registry = 'localhost:8123/'
    imageName = 'hello_world_war'
    registryCredentials = 'nexus'
    buildId = ''
  }
}
