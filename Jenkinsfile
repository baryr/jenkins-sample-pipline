pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'echo "Hello World"'
                sh '''
                    echo "Multiline shell steps works too"
                    ls -lah
                '''
                sh './gradlew clean build'
            }
        }
        stage('Test') {
            steps {
                //sh 'echo "Fail!"; exit 1'
                //sh 'echo "Success!"; exit 0'
                sh './gradlew check'
            }
        }
        stage('Deploy - Staging') {
            steps {
                sh 'echo "Deploy to staging!"'
            }
        }

        //ERROR: Test reports were found but none of them are new. Did leafNodes run?
        //stage('Sanity check') {
        //    steps {
        //        input "Does the staging environment look ok?"
        //    }
        //}

        stage('Deploy - Production') {
            steps {
                sh 'echo "Deploy to production!"'
            }
        }
    }
    post {
        always {
            echo 'This will always run'
            archive 'build/libs/**/*.jar'
            junit 'build/test-results/**/*.xml'
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
            //mail to: 'bartosz.roznowski@gmail.com',
            //     subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
            //     body: "Something is wrong with ${env.BUILD_URL}"
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}
