@Library('my-shared-library') _

pipeline {
    agent any 
    tools {
        jdk 'Java 17'
        maven 'Maven 3'
    }
    parameters {
        choice(name: 'action', choices:['create','delete'], description: 'choose the one create/destroy')
    }
    stages {
        stage('git checkout') {
            when { expression { params.action == 'create' } }
            steps {
                script {
                git branch: 'main', url: 'https://github.com/naveenroy65/Java_app_3.0.git'
                }
            }
        }
        stage('Unit Testing') {
            when { expression { params.action == 'create' } }
            steps {
                script {
                     mvnTest()
                }
            }
        }
        stage('Integration Testing') {
            when { expression { params.action == 'create'  } }
            steps {
                script {
                    mvnIntegrationTest()
                }
                
            }
        }
       """ stage('Static Code Analysis : sonarqube') {
            when { expression { params.action == 'create'  } }
            steps {
                script {
                    SonarQubecredentialId = 'sonar-api'
                    StaticCodeAnalysis(SonarQubecredentialId)
                }
            }
        }"""
        stage('Maven Build: maven') {
            when { expression { params.action == 'create'  } }
            steps {
                script {
                    mvnBuild()
                }
            }
        }
        
        
    }
}
