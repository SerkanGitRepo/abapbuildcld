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
//	stage ('Build') {
//	  git url: 'https://github.com/SerkanGitRepo/abapbuildcld'
//	  sh "mvn validate" 
//	}
//	
//	stage ('Integration') {
//		git url: 'https://github.com/SerkanGitRepo/abapbuildcld'
//		sh "mvn test"
//	}
	stage ('Acceptance') {
//		git url: 'https://github.com/SerkanGitRepo/TestMavenPrj.git'
//      sh 'docker run -d --network="host" testmavenprj:1 mvn -f /home/TestMavenPrj/pom.xml clean verify'
		sh 'docker run -i -v $(pwd):/opt/myapp -w /home/TestMavenPrj --network="host" testmavenprj:1 mvn -f /home/TestMavenPrj/pom.xml clean verify'
//		docker run -i -v `pwd`:/opt/myapp -w /opt/myapp -t mydockerimage 
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