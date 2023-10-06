pipeline {
    agent any
    tools {
        // Specify the name of the Maven installation configured in Jenkins
        maven 'mvn'
    }

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
        
/*    
        stage('Build') {
            steps {
                // Use 'mvn' command here
                bat '"C:\\apache-maven-3.9.4\\bin\\mvn" clean install -U'
            }
        }
*/
        stage('SonarQube Analysis') {
            environment {
                scannerHome = tool name: 'SonarScanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
            }
            steps {
                script {
                    def scannerHome = tool name: 'SonarScanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
                   /* def mvn = "mvn";*/
                    withSonarQubeEnv('bhushan') {
                        bat "${maven} clean verify sonar:sonar -Dsonar.projectKey=java2- -Dsonar.projectName='java2-'"

                    }
                }
            }
        }
    }
}
