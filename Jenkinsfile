pipeline {
	agent any 
	tools {
		maven 'maven3'
		jdk 'jdk-21'
	}
	environment {
		SONAR_HOME = tool 'sonar-scanner'
	}
	stages {
		stage('checkout') {
			steps {
				git branch: 'main', credentialsId: 'github', url: 'https://github.com/Ramlu/Multi-Tier-With-Database.git'
			}
		}
		stage('Compile') {
			steps {
				sh 'mvn clean compile'
			}
		}
		stage('Test') {
			steps {
				sh 'mvn test -DSkipTests'
			}
		}
        stage('Scan') {
            steps {
                sh 'trivy fs --format table -o fs.html .'
            }   
        } 
		// stage('Sonar Analysis') {
        //     steps {
        //         withSonarQubeEnv('sonar-server') {
        //             sh "${SONAR_HOME}/bin/sonar-scanner " +
        //                "-Dsonar.projectKey=bankapp " +
        //                "-Dsonar.projectName=BankApp " +
        //                "-Dsonar.sources=src/main/java " +
        //                "-Dsonar.tests=src/test/java " +
        //                "-Dsonar.java.binaries=target/classes " +
        //                "-Dsonar.junit.reportPaths=target/surefire-reports " +
        //                "-Dsonar.coverage.jacoco.xmlReportPaths=target/site/jacoco/jacoco.xml"
        //         }
        //     }
        // }
        // stage('Deploy') {
		// 	steps {
		// 		withMaven(globalMavenSettingsConfig: '5ecbebcf-4fa0-413f-a9de-1cd928c6b445', jdk: 'jdk-21', maven: 'maven3', mavenSettingsConfig: '', traceability: true) {
		// 			sh 'mvn deploy'
		// 		}
		// 	} 
		// }
		stage('Package') {
			steps {
				sh 'mvn package'
			}
		}
	}
}