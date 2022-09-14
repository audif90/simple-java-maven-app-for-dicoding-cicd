node {
    withDockerContainer(args'-v /root/.m2:/root/.m2', image:'maven:3-alpine')
    stage('build'){
        sh 'mvn -B -DskipTests clean package'
    }

    stage('test'){
        sh 'mvn test'
    }

    stage('deploy'){
        sh './jenkins/scripts/deliver.sh'
    }
}