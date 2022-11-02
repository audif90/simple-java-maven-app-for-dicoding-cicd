node {
    docker.image('maven:3-alpine').inside('-v /root/.m2:/root/.m2') {
        stage('build'){
            sh 'cp -r /home/Documents/dicoding/ioh/test/simple-java-maven-app-for-dicoding-cicd/* .'
            sh 'ls -alh'
            sh 'echo test'
            sh 'pwd'
            sh 'ls -alh'
            // withMaven(){
            // sh 'mvn "-B" "-DskipTests" "clean package" "-e" "-X" '   
            // }
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