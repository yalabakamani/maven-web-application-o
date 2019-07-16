// Powered by Infostretch 

timestamps {

node () {

	stage ('flikart-dev - Checkout') {
 	 checkout([$class: 'GitSCM', branches: [[name: '*/development']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'e93bf3fe-9b64-42dd-b45c-2da9cafeedf1', url: 'https://github.com/MithunTechnologiesDevOps/maven-web-application.git']]]) 
	}
	stage ('flikart-dev - Build') {
 			// Maven build step
	withMaven(maven: 'maven3.6.1') { 
 			if(isUnix()) {
 				sh "mvn clean  sonar:sonar deploy " 
			} else { 
 				bat "mvn clean  sonar:sonar deploy " 
			} 
 		} 
	}
}
}