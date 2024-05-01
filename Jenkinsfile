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
        stage("Test Stage"){
            steps{
                echo "----------- unit test started ----------"
                sh 'mvn surefire-report:report'
                echo "----------- unit test Completed ----------"
            }
        }
        stage("Artifact Publish") {
            steps {
                script {
                    echo '------------- Artifact Publish Started ------------'
                    def server = Artifactory.newServer url:"https://ourportal.jfrog.io/artifactory" ,  credentialsId:"jfrog-cred"
                    def properties = "buildid=${env.BUILD_ID},commitid=${GIT_COMMIT}";
                    def uploadSpec = """{
                        "files": [
                            {
                                "pattern": "staging/(*)",
                                "target": "soumya",
                                "flat": "false",
                                "props" : "${properties}",
                                "exclusions": [ "*.sha1", "*.md5"]
                            }
                        ]
                    }"""
                    def buildInfo = server.upload(uploadSpec)
                    buildInfo.env.collect()
                    server.publishBuildInfo(buildInfo)
                    echo '------------ Artifact Publish Ended -----------'  
                }
            }   
        }

    }
}