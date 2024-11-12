pipeline {
    agent {label 'usjenkins'}
    tools {
        maven '3.8.7'
    }
    
    stages {
        stage("Git Checkout") {
            steps {
                git branch: 'main', url: 'https://github.com/karthikdpai5u/test-petclinic-app.git'
            }
        }
        stage("Compile") {
            steps {
                sh "mvn compile"
            }
        }
        stage("Test") {
            steps {
                sh "mvn test -DskipTests=true"
            }
        }
        stage("Build") {
            steps {
                sh "mvn package -DskipTests=true"
            }
        }
        stage('Deploy') {
            steps {
                deploy adapters: [tomcat9(url: 'http://43.204.108.1:8585',
                            credentialsId: 'admin')],
                        war: 'target/*.war',
                        contextPath: 'app1'
            }
        }
    }
}
