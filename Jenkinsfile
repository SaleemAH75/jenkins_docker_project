pipeline{

    agent {label 'Jenkins-Agent'}

    tools{
        jdk "JAVA17"
        maven "MAVEN3"
    }

    stages{
        stage('cleanup workspace'){
            steps{
                cleanWs()
            }
        }

        stage('checkout scm'){
            steps{
                git branch: 'main', credentialsId: 'github', url:'https://github.com/SaleemAH75/jenkins_docker_project.git'
            }
        }

        stage('Build Application'){
            steps{
                sh 'mvn clean package'
            }
        }

        stage('Test Application'){
            steps{
                sh 'mvn test'
            }
        }

        stage('SonarQube analysis'){
            environment {
                scannerHome = tool 'sonar6.2'
            }
            steps{
                withSonarQubeEnv('sonarserver') {
                sh 'mvn clean package sonar:sonar'
              }
            }
        }

        stage('Quality gate'){
            steps{
                timeout(time: 1, unit: 'HOURS') {
                waitForQualityGate abortPipeline: true
              }
            }
        }
    }
}