node {
    docker.image('maven:3-alpine').inside('-v /root/.m2:/root/.m2') {
        stage('build'){
            git '/home/Documents/dicoding/ioh/simple-java-maven-app-for-dicoding-cicd'
            sh 'ls -all && pwd'
            withMaven(){
            sh 'mvn -B -DskipTests clean package'   
            }
        }

        stage('test'){
            withMaven(){
            sh 'mvn test'
            }
        }

        stage('Manual Approval'){
            input(message: "Lanjutkan ke tahap Deploy?")
        }

        stage('deploy'){
            sh './jenkins/scripts/deliver.sh'
            sh 'echo "Sleeping to wait until finish"'
            sh 'sleep 60s'
        }
    }
}
