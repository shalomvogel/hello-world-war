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
        sh '''export SONAR_TOKEN="INSERT_YOUR_TOKEN_HERE"
mvn verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar -Dsonar.projectKey=INSET_YOUR_PROJECT_KEY_HERE -Dsonar.organization=INSET_YOUR_ORGANIZATION_HERE -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=$SONAR_TOKEN'''
            }
        }
            stage('docker build') {
      steps {
        sh 'docker build -t hww-shalom:latest .'
      }
    }
      }
}


//     stage('docker tag') {
//       steps {
//         sh 'docker tag hello_world_war:latest 192.168.1.224:8123/hello_world_war:latest'
//       }
//     }

//     stage('docker push') {
//       steps {
//         script {
//           docker.withRegistry('http://192.168.1.224:8123', 'nexus') {
//             docker.build('hello_world_war').push('latest')
//           }
//         }

//       }
//     }

//   }
//   environment {
//     registry = '192.168.1.224:8123/'
//     imageName = 'hello_world_war'
//     registryCredentials = 'nexus'
//     buildId = ''
//   }
// }
