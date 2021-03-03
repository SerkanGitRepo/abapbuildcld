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
	def customImage
	def buildID
//	stage('Init'){
//		sh 'docker run -d -p 4545:4444 --name selenium-hubS selenium/hub'
//		sleep 2
//		sh 'docker run -d -p 4546:5900 --link selenium-hubS:hub selenium/node-chrome-debug'
//		sleep 2
//		sh 'docker run -d -p 5566:5900 --link selenium-hubS:hub selenium/node-firefox-debug'
//	}
	
//	stage ('Build') {
//		git url: 'https://github.com/SerkanGitRepo/abapbuildcld'
//		sh "mvn validate"
//	}
	
//	stage ('Integration') {
//		git url: 'https://github.com/SerkanGitRepo/abapbuildcld'
//		sh "mvn test"
//	}
	
	
	stage('Build Test Image'){
		git url: 'https://github.com/SerkanGitRepo/CC_BDD_TNG.git'
		//customImage = docker.build("testmvnprjtest:${env.BUILD_ID}")
		docker.build("test-paralel:1")
		sh 'docker-compose -f docker-compose.yml up -d' 
	}
	
	stage ('Acceptance') {
		sh 'docker run -i -v $(pwd):/opt/myapp -w /home/CC_BDD_TNG --network="host" test-paralel:1 mvn -f /home/CC_BDD_TNG/pom.xml clean verify'
//		sh 'docker cp $(docker ps -aq --filter "network=host"):/home/TestMavenPrj/target/site/serenity .'
		publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: true, reportDir: "/var/jenkins_home/workspace/SonPipelineSon/serenity", reportFiles: "index.html", reportName: "HTML Report", reportTitles: "Test Raporu"])
		sh 'docker rm $(docker ps -aq --filter "network=host")'
	}

//	stage('Terminate Docker Source'){
//		sh 'docker rm -f $(docker ps -aq --filter "ancestor=selenium/node-chrome-debug")'
//		sh 'docker rm -f $(docker ps -aq --filter "ancestor=selenium/node-firefox-debug")'
//		sh 'docker rm -f $(docker ps -aq --filter "ancestor=selenium/hub")'
//	}
}



	

//piperPipeline script: this
//node() {
//	stage('Acceptance') {
//		seleniumExecuteTests (script: this) {
//			git url: 'https://github.com/SerkanGitRepo/TestMavenPrj.git'
//			sh '''mvn clean verify'''
//		}
//}