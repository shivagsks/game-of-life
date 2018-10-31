node('master') {
    stage('Checkout') {
    git 'https://github.com/arjunkundur/game-of-life.git'
input message: 'Please give your valuable input', parameters: [choice(choices: ['Approved', 'Declined', 'Pause'], description: '', name: 'Input')]

}
 stage('SonarQube analysis') {
    // requires SonarQube Scanner 2.8+
    def scannerHome =tool name: 'Sonar-Scanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
    withSonarQubeEnv('My SonarQube Server') {
      sh "${scannerHome}/bin/sonar-scanner"
}
}

stage('Build') {
     def mvnHome=tool name: 'maven', type: 'maven'
	 def mvnCMD="${mvnHome}/bin/mvn"
	 sh "${mvnCMD} install"
input message: 'Please give your valuable input', parameters: [choice(choices: ['Approved', 'Declined', 'Pause'], description: '', name: 'Input')]

}
stage('Nexus_Deploy') {
nexusArtifactUploader artifacts: [[artifactId: 'dev', classifier: '', file: 'gameoflife-web/target/gameoflife.war', type: 'war']], credentialsId: '9b18dbb7-942e-4ca1-a0ff-ec2ef32d929a', groupId: 'dev', nexusUrl: '13.232.243.180:8081/nexus', nexusVersion: 'nexus2', protocol: 'http', repository: 'pipeline', version: '1.1'

}
}


