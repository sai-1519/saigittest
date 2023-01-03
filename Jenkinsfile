pipeline {
    agent any
    tools{
        maven 'Maven3'
    }

    stages {
        stage('source_stage') {
            steps {
                git credentialsId: 'git', url: 'https://github.com/sai-1519/saigittest.git'
            }
        }
      stage('compile_stage') {
            steps {
                sh'mvn clean compile'
            }
        }
     stage('test_stage') {
            steps {
               sh'mvn clean test'
            }
        }
     stage('sonar_analysis') {
            steps {
                withSonarQubeEnv('sonar'){
                    sh 'mvn clean package sonar:sonar'
                }
            }
        }
        stage('Deploy_Stage') {
            steps {
               deploy adapters: [tomcat9(credentialsId: 'Tomcat', path: '', url: 'http://54.221.2.13:8090/')], contextPath: null, war: '**/*.war'
            }
        }
    }
}

