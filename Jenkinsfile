node {
    docker.image('maven:3-alpine').inside('-v /root/.m2:/root/.m2') {
        stage('build'){
            /** Jenkinsnya ada bug, dicoba dengan repo yg sama kadang konten dari projeknya ke copy kadang kosong.
            Anehnya, Jenkinsfile tetap terdeteksi. Ini tidak terjadi di submission pertama padahal repo yang sama.
            Sudah dites di EC2 maupun local, tetap bug seperti ini.
            Maka dari itu utk memastikan tidak terjadi terus menerus, saya menerapkan pull langsung ke online repo. **/
            git 'https://github.com/audif90/simple-java-maven-app-for-dicoding-cicd'
            sh 'chmod +x jenkins/scripts/deliver.sh'
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
