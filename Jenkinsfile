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
                echo "-----Build_started by soumya------"
                sh "/opt/apache-maven-3.9.6/bin/mvn clean package "
                echo "-------Build_Ended by soumya-----------"
            }
        }
        stage('SonarQube analysis') {
            environment {
                scannerHome = tool 'sonar-scanner-meportal'
            }
            steps{
                withSonarQubeEnv('sonar-server-meportal') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }
        stage("Quality Gate"){
            steps {
                script {
                    timeout(time: 1, unit: 'HOURS') { 
                        def qg = waitForQualityGate() 
                        if (qg.status != 'OK') {
                            error "Pipeline aborted due to quality gate failure: ${qg.status}"
                        }
                    }
                }
            }
        }

    }
}