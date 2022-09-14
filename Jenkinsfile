// node {
//     stage('build'){
//         docker.image('maven:3-alpine').inside('-v /root/.m2:/root/.m2') {
//             sh 'ls -all'
//             sh 'pwd'
//             sh 'mvn -B -DskipTests clean package'
//         }
//     }

//     stage('test'){
//         sh 'mvn test'
//     }

//     stage('deploy'){
//         sh './jenkins/scripts/deliver.sh'
//     }
// }

pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests -Denforcer.skip=true clean package '
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}
