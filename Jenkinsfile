pipeline {
    agent any
    tools {
        maven "maven"
    }
    stages {
        // stage('Build') { 
        //     steps {
        //         echo 'Building..'
        //         sh 'mvn -B -DskipTests clean package' 
        //     }
        // }
        stage('Build') {
            steps {
                dir("/var/lib/jenkins/workspace/module6/my-app") {
                sh 'mvn -B -DskipTests clean package'
                }
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}

