pipeline{
    agent{
        dockerContainer "vikasprince/jenkinsagent"
    }
    
    tools{
        maven "maven"
    }
    
    stages{
        stage("checkout"){
            steps{
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/Vikas-Prince/java-test-maven.git'
            }
        }
        
        stage("compile"){
            steps{
                sh "mvn compile"
            }
        }
        
        stage("test"){
            steps{
                sh "mvn test"
            }
        }
        
        stage("build"){
            steps{
                sh "mvn clean package"
            }
        }
        
        stage("deploy"){
            steps{
                withMaven(globalMavenSettingsConfig: 'nexus', jdk: '', maven: 'maven', mavenSettingsConfig: '', traceability: true) {
                    sh "mvn deploy"
                }
            }
        }
    }
    
    post {
        always {
            emailext(
                subject: "Build ${currentBuild.currentResult}: ${env.JOB_NAME} ${env.BUILD_NUMBER}",
                body: '''
                Hi Team,
                
                Please find the build artifact attached.
                
                Regards,
                Jenkins
                
                ''',
                
                attachLog: true,
                attachmentsPattern: 'target/*.jar',
                to: 'vikasprince30809@gmail.com',
                replyTo: 'no-reply@gmail.com',
                from: "vikas@jenkins.com"
            )
        }

        success {
            echo "Build succeeded."
        }

        failure {
            echo "Build failed."
        }
    }
}
