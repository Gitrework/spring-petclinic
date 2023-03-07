pipeline {
    agent { label 'SONAR-NODE' }
    triggers { pollSCM ('* * * * *') }
    parameters {
        choice(name: 'MAVEN_GOAL', choices: ['package', 'install', 'clean'], description: 'Maven Goal')
    }
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
                sh "mvn ${params.MAVEN_GOAL}"
            }
        }
        stage('sonar analysis') {
            steps {
                  withSonarQubeEnv('SONAR_CLOUD') {
                    sh 'mvn verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar -Dsonar.projectKey=narayanasonar_sonarproject -Dsonar.organization=narayanasonar'
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