pipeline {
    agent { label 'JDK_17' }
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/Gitrework/spring-petclinic.git',
                    branch: 'main'
            }
        }
        stage('package') {
            tools {
                jdk 'JAVA-17-JDK'
            }
            steps {
                sh 'mvn clean package'
            }
        }
        stage('sonar analysis') {
            steps {
                // performing sonarqube analysis with "withSonarQubeENV(<Name of Server configured in Jenkins>)"
                withSonarQubeEnv('SONAR_CLOUD') {
                    sh 'mvn clean package verify sonar:sonar -Dsonar.login=347947eb6562c86f329029f668687056135cd4e5 -Dsonar.organization=SONAR_DEVELOP1'
                }
            }
        }
        stage('post build') {
            steps {
                archiveArtifacts artifacts: '**/*.jar',
                                 onlyIfSuccessful: true
                junit testResults: '**/TEST-*.xml'
            }
        }
    }
} 