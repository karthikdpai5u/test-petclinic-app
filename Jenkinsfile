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
                deploy adapters: [tomcat9(url: 'http://3.110.183.53:8080/',
                            credentialsId: '0b69141a-312b-44f7-894b-68e947ea4353')],
                        war: 'target/*.war',
                        contextPath: 'app1'
            }
        }
    }
}
