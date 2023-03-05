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
            stage('buld') {
                  steps{
                        archiveArtifacts artifacts:  '**/*.txt',
                                 onlyIfSuccessful: true
                        junit testResults: '**/surefire-reports/TEST-*.xml'
                  }
            }

      }
}