pipeline {
    agent { label 'server-developement' }
    tools {
        maven "MAVEN"  // Ensure "MAVEN" is the name configured in Global Tool Configuration
    }

    stages {
        stage('Checkout') {
            steps {
                // Use the correct repository URL
                git url: 'https://github.com/SofianHaidour/E-Health_Jenkins.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                // Run Maven build (skip tests for faster builds, can be modified based on your need)
                sh 'mvn -B -DskipTests clean package'
            }
        }

        stage('Static Analysis') {
            steps {
                // Ensure the static analysis tools are correctly installed and configured in Jenkins
                recordIssues sourceCodeRetention: 'LAST_BUILD', tools: [checkStyle(), pmdParser(), findBugs()]
            }
        }

        // Uncomment this stage if you want to deploy after building
        /*
        stage('Deploy') {
            steps {
                // Example of deployment using SCP and SSH (adjust to your needs)
                sh '''
                JAR_FILE=target/ehealth-back-1.0.jar
                scp $JAR_FILE $TARGET_MACHINE:$TARGET_DIR
                ssh $TARGET_MACHINE "cd $TARGET_DIR && java -jar $JAR_FILE"
                '''
            }
        }
        */
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}
