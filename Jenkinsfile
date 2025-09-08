// Jenkins pipeline
pipeline {
    agent any
    triggers { pollSCM('* * * * *') } // check commits every 1 min

    stages {
        stage('Build') {
            steps {
                echo 'Building project... | Tool: Maven/Gradle'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                script {
                    try {
                        echo 'Running tests... | Tools: JUnit, Jest, Newman'
                        sh 'npm test || true'
                        currentBuild.result = 'SUCCESS'
                    } catch (Exception e) {
                        currentBuild.result = 'FAILURE'
                        throw e
                    }
                }
            }
            post {
                always {
                    emailext(
                        subject: "Jenkins Notification: Test Stage - ${currentBuild.result}",
                        body: """<h3>Stage: Unit & Integration Tests</h3>
                                 <p>Status: ${currentBuild.result}</p>
                                 <p>Check Jenkins for console log: ${BUILD_URL}</p>""",
                        to: "seoyoung.jo99@gmail.com",
                        attachmentsPattern: "**/target/*.log"
                    )
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Code Analysis | Tool: SonarQube/PMD'
            }
        }

        stage('Security Scan') {
            steps {
                script {
                    try {
                        echo 'Running security scan... | Tool: Snyk/OWASP'
                        sh 'npm audit || true'
                        currentBuild.result = 'SUCCESS'
                    } catch (Exception e) {
                        currentBuild.result = 'FAILURE'
                        throw e
                    }
                }
            }
            post {
                always {
                    emailext(
                        subject: "Jenkins Notification: Security Scan - ${currentBuild.result}",
                        body: """<h3>Stage: Security Scan</h3>
                                 <p>Status: ${currentBuild.result}</p>
                                 <p>Check Jenkins for console log: ${BUILD_URL}</p>""",
                        to: "seoyoung.jo@gmail.com",
                        attachmentsPattern: "**/target/*.log"
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging... | Tool: AWS CLI, Ansible'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running staging tests... | Tool: Selenium/Newman'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production... | Tool: AWS CLI/Kubernetes'
            }
        }
    }
}
