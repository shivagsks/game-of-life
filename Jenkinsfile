node('master') {
    stage('Checkout') {
    git 'https://github.com/arjunkundur/game-of-life.git'

}
stage('Build') {
     def mvnHome=tool name: 'maven', type: 'maven'
	 def mvnCMD="${mvnHome}/bin/mvn"
	 sh "${mvnCMD} install"

}
stage('Nexus_Deploy') {
nexusArtifactUploader artifacts: [[artifactId: 'dev', classifier: '', file: 'gameoflife-web/target/gameoflife.war', type: 'war']], credentialsId: '9b18dbb7-942e-4ca1-a0ff-ec2ef32d929a', groupId: 'dev', nexusUrl: '13.232.243.180:8081/nexus', nexusVersion: 'nexus2', protocol: 'http', repository: 'pipeline', version: '1.0'

}
}


