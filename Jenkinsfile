#!/usr/bin/env groovy 

/*
 * This file bootstraps the codified Continuous Delivery pipeline for extensions of SAP solutions such as SAP S/4HANA.
 * The pipeline helps you to deliver software changes quickly and in a reliable manner.
 * A suitable Jenkins instance is required to run the pipeline.
 * The Jenkins can easily be bootstraped using the life-cycle script located inside the 'cx-server' directory.
 *
 * More information on getting started with Continuous Delivery can be found here: https://sap.github.io/jenkins-library/
 */

@Library('piper-lib-os') _

piperPipeline script: this

//pipeline {
//	agent {
//		docker {
//			image 'maven:3.6-jdk-8' 
//			args '-v /root/.m2:/root/.m2'
//		}
//	}
//	stages {
//		stage('git') {
//			steps{
//				git credentialsId: 'Git_Serkan_Repo', url: 'https://github.com/SerkanGitRepo/abapbuildcld.git'
//			}
//		}
//		
//		stage('Build') {
//			steps {
//				sh 'mvn -version'
//				sh 'mvn clean package'
//			}
//		}
//	}
//}