pipeline {
    agent any

    tools {
        // Install the Maven version configured as "Fill with the name of given to the maven tool install in config" and add it to the path.
        maven 'MavenInstall'
    }

     stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/JFMcKay/MyDevPizza.git'

                // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true package"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
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
    }
}
