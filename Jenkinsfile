pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
                }
            }
        stage('SCM') {
            steps {
                // Checkout the code from Git
                checkout([$class: 'GitSCM', 
                          branches: [[name: '*/master']], 
                          doGenerateSubmoduleConfigurations: false, 
                          extensions: [], 
                          submoduleCfg: [], 
                          userRemoteConfigs: [[url: 'https://github.com/BhushanShete/artigo-boas-praticas-medium.git']]])
            }
        }

        stage('SonarQube Analysis') {
            environment {
                scannerHome = tool name: 'SonarScanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
            }
            steps {
                script {
                    def scannerHome = tool name: 'SonarScanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
                    def mvn = tool 'mvn';
                    withSonarQubeEnv('bhushan') {
                        bat "${mvn} clean verify sonar:sonar -Dsonar.projectKey=bhushanJAVA -Dsonar.projectName='bhushanJAVA'"

                    }
                }
            }
        }
    }
}
