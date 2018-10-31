node('master') {

stage('Checkout') {
	git 'https://github.com/arjunkundur/game-of-life.git'
}

stage('Build') {
     def mvnHome=tool name: 'Maven', type: 'maven'
	 def mvnCMD="${mvnHome}/bin/mvn"
	 sh "${mvnCMD} install"
}

stage('Nexus_Deploy') {
	nexusArtifactUploader artifacts: [[artifactId: 'dev', classifier: '', file: 'gameoflife-web/target/gameoflife.war', type: 'war']], credentialsId: '44e5c24c-2ec4-4ac4-a599-58183becda76', groupId: 'dev', nexusUrl: '54.191.210.253:8081/nexus', nexusVersion: 'nexus2', protocol: 'http', repository: 'new', version: '$BUILD_ID'	
}

stage('Ansible_Playbook') {
	ansiblePlaybook inventory: '/home/ubuntu/inventory', playbook: 'playbook.yml'
	
}


}

