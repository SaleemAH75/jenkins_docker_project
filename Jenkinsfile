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
    }
}