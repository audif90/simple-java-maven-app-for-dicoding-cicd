node {
    stage('build'){
        docker.image('maven:3-alpine').withRun('-v /root/.m2:/root/.m2') {
            sh 'mvn -B -DskipTests clean package'
        }
    }

    stage('test'){
        sh 'mvn test'
    }

    stage('deploy'){
        sh './jenkins/scripts/deliver.sh'
    }
}