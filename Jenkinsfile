pipeline {
    agent { label 'SONAR-NODE' }
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/Gitrework/spring-petclinic.git',
                    branch: 'main'
            }
        }
        stage('package') {
             tools {
                    jdk 'JAVA-11-JDK'
                  }
            steps {
                 sh 'mvn package'
           }
        }
        stage('post build') {
            steps {
                archiveArtifacts artifacts: '**/*.txt',
                                 onlyIfSuccessful: true
                junit testResults: '**/surefire-reports/TEST-*.xml'
            }
        }
    }
}