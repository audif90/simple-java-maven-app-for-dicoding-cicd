node {
    docker.image('maven:3-alpine').inside('-v /root/.m2:/root/.m2') {
        stage('build'){
                withMaven(){
                sh 'mvn -B -DskipTests clean package'   
                }
            }

        stage('test'){
            withMaven(){
            sh 'mvn test'
            }
        }

        stage('deploy'){
            sh './jenkins/scripts/deliver.sh'
        }
    }
}