pipeline {
  agent any

  stages {
      stage('Build Artifact') {
            steps {
              sh "mvn clean package -DskipTests=true"
              archive 'target/*.jar' 
            }
        }
        
    //   stage('Unit Tests and jacoco') {
    //         steps {
    //           sh "mvn test"
    //   }
    //   // post{
    //   //     always{
    //   //       junit 'target/surefire-reports/*.xml'
    //   //       jacoco execPattern: 'target/jacoco.exec'
    //   //     }
    //   // }
    // }

    // stage('Mutation Tests - PIT') {
    //       steps {
    //         sh "mvn org.pitest:pitest-maven:mutationCoverage"
    //   }

    // }

    stage('SonarQube - SAST') {
          steps {
            sh "mvn clean verify sonar:sonar -Dsonar.projectKey=devsecops-demo-spingboot -Dsonar.projectName='devsecops-demo-spingboot' -Dsonar.host.url=http://asasatech.eastus.cloudapp.azure.com:9000 -Dsonar.token=sqp_47aaaa7279928a11d08a64d20f870df7abecf0f8"

         }
    

       }
    stage('Vulnerability Scan - Docker ') {
          steps {
            sh "mvn dependency-check:check"
      }
      // post {
      //   always {
      //     dependencyCheckPublisher pattern: 'target/dependency-check-report.xml'
      //   }
      // }
    }
  }

}