pipeline {
    agent {
        node {
            label "jenkins-slave-node"
        }
    }
    stages {
        stage ('CheckOut Code') {
            steps {
                echo "------Check_Out_Started------"
                git branch: "main" , url: "https://github.com/technicalsoumya/java-web-app.git"
                echo "--------Check_Out_End--------"
            }
        }
        stage ('Build Code') {
            steps {
                echo "-----Build_started------"
                sh "/opt/apache-maven-3.9.6/bin/mvn clean package "
                echo "-------Build_End-----------"
            }
        }

    }
}