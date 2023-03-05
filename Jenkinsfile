pipeline{
      agent { label 'SONAR-NODE' }
      stages {
            stage('vcs') {
                  steps{
                        git url: 'https://github.com/Gitrework/spring-petclinic.git',
                            branch: 'main'
                  }
            } 
            stage('package') {
                  tools {
                        jdk 'JAVA-17-JDK'
                  }   
                  steps{
                        sh 'mvn package'
                  }                  
            }
            stage('sonar analysis') {
                  steps {
                // performing sonarqube analysis with "withSonarQubeENV(<Name of Server configured in Jenkins>)"
                        withSonarQubeEnv('SONARQUBE') {
                        sh 'mvn clean package sonar:sonar -Dsonar.organization=lakshminarayana'
                        }
                  }
           }
            stage('buld') {
                  steps{
                        archiveArtifacts artifacts:  '**/target/spring-petclinic-3.0.0-SNAPSHOT.jar',
                                 onlyIfSuccessful: true
                        junit testResults: '**/surefire-reports/TEST-*.xml'
                  }
            }

      }
}