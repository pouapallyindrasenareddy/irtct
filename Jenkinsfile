pipeline {
    agent any

    tools {
        maven 'MAVEN_HOME'       // Configure Maven in Jenkins -> Global Tool Config
        jdk 'JAVA_HOME'          // Configure JDK in Jenkins -> Global Tool Config
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/your-repo/your-project.git'
            }
        }

        stage('Build with Maven') {
            steps {
                sh "mvn clean install"
            }
        }

        stage('Run Unit Tests') {
            steps {
                sh "mvn test"
            }

            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }

        stage('Package Artifact') {
            steps {
                sh "mvn package"
            }
            post {
                success {
                    archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
                }
            }
        }
    }

    post {
        always {
            echo "Pipeline finished!"
        }
    }
}

