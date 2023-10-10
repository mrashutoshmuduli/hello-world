pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven-3.2"
        jdk "jdk11"
    }

    stages {
        stage('Build') {
            steps {
                
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/mrashutoshmuduli/hello-world.git'
                sh "mvn -Dmaven.test.failure.ignore=true clean install"
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
          }
          stage ('Deploy'){
            steps {
              sh 'echo \'hello world application deploymenty\''
              sh 'java -jar ./target/spring-boot-2-hello-world-1.0.2-SNAPSHOT.jar --server.port=8081'
                }
          }
        }
    }
