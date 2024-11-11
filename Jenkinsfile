pipeline {
    agent {
        label 'usjenkins'
    }
    
    tools {
        maven 'maven'
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
                deploy adapters: [tomcat10(url: 'http://13.233.144.3:8585',
                            credentialsId: 'admin')],
                        war: 'target/*.war',
                        contextPath: 'app1'
            }
        }
    }
}
