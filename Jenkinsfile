node {
    docker.image('maven:3-alpine').inside('-v /root/.m2:/root/.m2') {
        stage('build'){
            withMaven(){
            sh 'mvn "-B" "-DskipTests" "clean package" "-e" "-X" '   
            }
        }

        stage('test'){
            sh 'ls -alh'
            withMaven(){
            sh 'mvn test'
            }
        }

        stage('deploy'){
            sh './jenkins/scripts/deliver.sh'
        }
    }
}