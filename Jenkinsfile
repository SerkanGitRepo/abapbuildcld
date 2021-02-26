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
//		sh 'docker run -d -p 5900:5900 --link selenium-hubS:hub selenium/node-chrome-debug'
//		sh 'docker run -d -p 5901:5900 --link selenium-hubS:hub selenium/node-firefox-debug'
//	}
	
	stage ('Build') {
		git url: 'https://github.com/SerkanGitRepo/abapbuildcld'
		sh "mvn validate"
	}
	
	stage ('Integration') {
		git url: 'https://github.com/SerkanGitRepo/abapbuildcld'
		sh "mvn test"
	}
	
	
	stage('Build Test Image'){
		git url: 'https://github.com/SerkanGitRepo/TestMavenPrj.git'
		//customImage = docker.build("testmvnprjtest:${env.BUILD_ID}")
		docker.build("testmvnprjtest:1")
	}
	
	stage ('Acceptance') {
		sh 'docker run -i -v $(pwd):/opt/myapp -w /home/TestMavenPrj --network="host" testmvnprjtest:1 mvn -f /home/TestMavenPrj/pom.xml clean verify'
//		sh 'docker cp $(docker ps -aq --filter "network=host"):/home/TestMavenPrj/target/site/serenity .'
		publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: true, reportDir: "/var/jenkins_home/workspace/SonPipelineSon/serenity", reportFiles: "index.html", reportName: "HTML Report", reportTitles: "Test Raporu"])
		sh 'docker rm $(docker ps -aq --filter "network=host")'
	}
}



	

//piperPipeline script: this
//node() {
//	stage('Acceptance') {
//		seleniumExecuteTests (script: this) {
//			git url: 'https://github.com/SerkanGitRepo/TestMavenPrj.git'
//			sh '''mvn clean verify'''
//		}
//}