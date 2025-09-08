pipeline {
    agent any
    // hello world!

    stages {
        stage('Stage 1: Build') {
            steps {
                echo '==================== Stage 1: Build ===================='
                echo 'Task: Compile the source code, resolve dependencies, and package the application.'
                echo 'Example Tool: Maven (Java) or Gradle (multi-language build automation).'
                echo 'Outcome: A build artifact (e.g., .jar, .war, or .zip) is generated.'
                echo '========================================================'
            }
        }

        stage('Stage 2: Unit and Integration Tests') {
            steps {
                echo '==================== Stage 2: Unit and Integration Tests ===================='
                echo 'Task: Run unit tests on individual components and integration tests across modules.'
                echo 'Tools: JUnit (Java), Jest/Mocha (JavaScript), or Newman (API testing).'
                echo 'Outcome: Verify correctness of functions and confirm components work together.'
                echo '============================================================================'
            }
        }

        stage('Stage 3: Code Analysis') {
            steps {
                echo '==================== Stage 3: Code Analysis ===================='
                echo 'Task: Perform static code analysis to detect bugs, enforce coding standards, and improve maintainability.'
                echo 'Tools: SonarQube (industry standard), PMD, or Checkstyle.'
                echo 'Outcome: A quality report highlighting issues and best practice compliance.'
                echo '================================================================'
            }
        }

        stage('Stage 4: Security Scan') {
            steps {
                echo '==================== Stage 4: Security Scan ===================='
                echo 'Task: Scan source code and dependencies for vulnerabilities and insecure configurations.'
                echo 'Tools: OWASP Dependency-Check or Snyk.'
                echo 'Outcome: Security report identifying critical, high, medium, and low vulnerabilities.'
                echo '================================================================'
            }
        }

        stage('Stage 5: Deploy to Staging') {
            steps {
                echo '==================== Stage 5: Deploy to Staging ===================='
                echo 'Task: Deploy the build artifact into a staging environment (mirrors production).'
                echo 'Tools: AWS CLI, Ansible, or SSH for deployment automation.'
                echo 'Outcome: Application is available in a controlled staging server for further testing.'
                echo '===================================================================='
            }
        }

        stage('Stage 6: Integration Tests on Staging') {
            steps {
                echo '==================== Stage 6: Integration Tests on Staging ===================='
                echo 'Task: Execute automated end-to-end and integration tests in the staging environment.'
                echo 'Tools: Selenium (UI testing), Postman/Newman (API regression testing).'
                echo 'Outcome: Confidence that the system behaves correctly under production-like conditions.'
                echo '================================================================================'
            }
        }

        stage('Stage 7: Deploy to Production') {
            steps {
                echo '==================== Stage 7: Deploy to Production ===================='
                echo 'Task: Deploy the verified and tested application into the production environment.'
                echo 'Tools: AWS CLI, Ansible, or Kubernetes (for container orchestration).'
                echo 'Outcome: Application is live and accessible to end users.'
                echo '======================================================================'
            }
        }
    }

    post {
        success {
            echo '🎉 Pipeline completed successfully. All stages executed as designed.'
        }
        failure {
            echo '❌ Pipeline failed. Please check the logs above for details.'
        }
    }
}
