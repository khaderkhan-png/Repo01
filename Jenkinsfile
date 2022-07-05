pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "MAVEN_HOME"
        jdk "JAVA_HOME"
    }
    triggers {
         pollSCM('H/2 * * * *')
     }
    stages {
	    
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git branch: 'main', url: 'https://github.com/khaderkhan-png/Repo01.git'

                // Run Maven on a Unix agent.
                //sh "mvn -Dmaven.test.failure.ignore=true clean package"

                // To run Maven on a Windows agent, use
                bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }

        }
        stage('deploy'){
            steps{
                deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://localhost:8082/')], contextPath: 'maven-web-application(P01)', onFailure: false, war: '**/*war'
            }
		}
        }
        
   }

