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
                echo "Build_started_"
                sh "/opt/maven/bin/mvn clean package "
                echo "-------Build_End-----------"
            }
        }

    }
}