#!/usr/bin/env groovy 

/*
 * This file bootstraps the codified Continuous Delivery pipeline for extensions of SAP solutions such as SAP S/4HANA.
 * The pipeline helps you to deliver software changes quickly and in a reliable manner.
 * A suitable Jenkins instance is required to run the pipeline.
 * The Jenkins can easily be bootstraped using the life-cycle script located inside the 'cx-server' directory.
 *
 * More information on getting started with Continuous Delivery can be found here: https://sap.github.io/jenkins-library/
 */

//@Library('piper-lib-os') _

node {
	
//	stage ('Build Project') {
//		git url: 'https://github.com/SerkanGitRepo/abapbuildcld'
//		sh "mvn validate"
//	}
//	
//	stage ('Integration') {
//		git url: 'https://github.com/SerkanGitRepo/abapbuildcld'
//		sh "mvn test"
//	}

	stage('Init Test Environment'){
		git url: 'https://github.com/SerkanGitRepo/CC_BDD_TNG.git'
		sh 'docker-compose -f docker-compose.yml up -d'
	}
	
	stage('Build Test Image'){
		git url: 'https://github.com/SerkanGitRepo/CC_BDD_TNG.git'
		//customImage = docker.build("testmvnprjtest:${env.BUILD_ID}")
		docker.build("test-paralel:1")
	}
	 
	stage ('Smoke Test') {
		sh 'docker run -i -v $(pwd):/opt/myapp -w /home/CC_BDD_TNG --network="host" test-paralel:1 mvn -f /home/CC_BDD_TNG/pom.xml clean test -fn'
////	sh 'docker cp $(docker ps -aq --filter "network=host"):/home/TestMavenPrj/target/site/serenity .'
		publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: true, reportDir: "/var/jenkins_home/workspace/SonPipelineSon/reports", reportFiles: "index.html", reportName: "HTML Report", reportTitles: "Test Raporu"])
//		sh 'docker rm $(docker ps -aq --filter "network=host")'
	}

	stage('Terminate Docker Source'){
		sh 'docker rm -f $(docker ps -aq --filter "ancestor=selenium/node-chrome-debug")'
		sh 'docker rm -f $(docker ps -aq --filter "ancestor=selenium/node-firefox-debug")'
		sh 'docker rm -f $(docker ps -aq --filter "ancestor=selenium/hub")'
	}
	
//	stage('Publis SAP CF'){
//		git url: 'https://github.com/SerkanGitRepo/abapbuildcld'
//		pushToCloudFoundry (
//			cloudSpace: 'dev', 
//			credentialsId: 'CF_IDENTITY_FOR_JENKINS', 
//			organization: 'a004cb52trial', 
//			target: 'https://api.cf.eu10.hana.ondemand.com',
//			manifestChoice: [manifestFile: 'manifest.yml']
//			)
//	}
	
}
