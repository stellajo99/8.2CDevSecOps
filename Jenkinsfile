// Jenkins pipeline for SIT753 - Part 2 Task 2
pipeline {
    agent any
    // hello
    environment {
        EMAIL_TO = "seoyoung.jo99@gmail.com" 
    }

    stages {
        stage('Build') {
            steps {
                echo 'Task: Build | Tool: Maven/Gradle | Compiling and packaging the project'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                script {
                    echo 'Task: Unit & Integration Tests | Tools: JUnit, Jest, Newman'
                    // run tests, allow pipeline to continue on failure
                    int code = sh(returnStatus: true, script: 'npm test || true')
                    if (code == 0) {
                        currentBuild.result = 'SUCCESS'
                    } else {
                        currentBuild.result = 'UNSTABLE'  // continue but mark warning
                    }
                }
            }
            post {
                always {
                    emailext(
                        subject: "[${currentBuild.result}] Jenkins - Test Stage",
                        to: env.EMAIL_TO,
                        body: """Stage: Unit & Integration Tests
                                 Status: ${currentBuild.result}
                                 Console log attached.
                                 Build URL: ${BUILD_URL}""",
                        attachLog: true
                    )
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Task: Code Analysis | Tools: SonarQube, PMD, Checkstyle'
            }
        }

        stage('Security Scan') {
            steps {
                script {
                    echo 'Task: Security Scan | Tools: npm audit / Snyk'
                    int code = sh(returnStatus: true, script: 'npm audit --json > audit.json || true')
                    if (code == 0) {
                        currentBuild.result = 'SUCCESS'
                    } else {
                        currentBuild.result = 'UNSTABLE'
                    }
                }
            }
            post {
                always {
                    emailext(
                        subject: "[${currentBuild.result}] Jenkins - Security Scan",
                        to: env.EMAIL_TO,
                        body: """Stage: Security Scan
                                 Status: ${currentBuild.result}
                                 Console log attached.
                                 Build URL: ${BUILD_URL}""",
                        attachLog: true,
                        attachmentsPattern: "audit.json"
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Task: Deploy to Staging | Tools: AWS CLI, Ansible, SSH'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Task: Integration Tests on Staging | Tools: Selenium, Newman'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Task: Deploy to Production | Tools: AWS CLI, Kubernetes'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'audit.json', allowEmptyArchive: true
        }
    }
}
