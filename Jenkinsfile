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
                          userRemoteConfigs: [[url: 'https://github.com/BhushanShete/sonar-scanner-maven.git']]])
            }
        }

        stage('SonarQube Analysis') {
            environment {
                scannerHome = tool name: 'SonarScanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
            }
            steps {
                script {
                    bat "mvn clean install -U"
                    def scannerHome = tool name: 'SonarScanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
                    def mvn = tool 'mvn';
                    withSonarQubeEnv('bhushan') {
                        bat "${mvn} clean verify sonar:sonar -Dsonar.projectKey=java2- -Dsonar.projectName='java2-'"

                    }
                }
            }
        }
    }
}
