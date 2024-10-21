pipeline{
  agent any

  tools{
    maven 'maven3'
  }

  stages{
    
    stage("Download the code"){
      steps{
          git branch: 'main', url: 'https://github.com/Vikas-Prince/java-test-maven.git'
      }
    }

    stage("Compile the code"){
      steps{
        sh 'mvn compile'
      }
    }

    stage("Run the Test Cases"){
      steps{
        sh 'mvn test'
      }
    }

    stage("Build the artifacts"){
      steps{
        sh 'mvn clean package'
      }
    }
    
  }
}
