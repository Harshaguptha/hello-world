#!/usr/bin/env groovy

@Library('shared-library@master') _ //master or whatever branch

pipeline{
      agent any

        stages{
		    stage('check out'){
                steps{
                    script{
		    	        checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/Harshaguptha/hello-world.git']]])
                      	  }
               	     }  
                 }	
            stage('maven build'){
                steps{
                    script{
		    	        sh "mvn clean install"
                      	  }
               	     }  
                 }	
  
            stage ('Check logs') {
                steps {
                    filterLogs ('WARNING', 1)
                    }
                }
            stage('Artifacts to S3'){
                steps{
                    script {
		    }sh ''BuildName="version-$BUILD_NUMBER"
				BucketName="samplehellow/Shared-Lib"
				zip -r $BuildName.zip *
				aws s3 cp $BuildName.zip s3:$BucketName --region ap-south-1''
		    	    //s3Upload consoleLogLevel: 'INFO', dontSetBuildResultOnFailure: false, dontWaitForConcurrentBuildCompletion: false, entries: [[bucket: 'samplehellow/Shared-Lib', excludedFile: '', flatten: false, gzipFiles: false, keepForever: false, managedArtifacts: false, noUploadOnFailure: false, selectedRegion: 'ap-south-1', showDirectlyInBrowser: false, sourceFile: '**/webapp/target/*.war', storageClass: 'STANDARD', uploadFromSlave: false, useServerSideEncryption: false]], pluginFailureResultConstraint: 'FAILURE', profileName: 'S3Deploy', userMetadata: []
			    	}
			    }
            }
		
        }	       	     	         
}
