pipeline {
    agent any

    environment {
        // Define environment variables here
        MY_ENV_VAR = 'Production'
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    // Clone the Git repository's master branch
                    def gitRepoUrl = 'https://github.com/cloudwithsaraansh/check-weather-repo.git'

                    checkout([$class: 'GitSCM', 
                        branches: [[name: '*/main']], 
                        userRemoteConfigs: [[url: gitRepoUrl]], 
                        extensions: [[$class: 'CleanBeforeCheckout'], [$class: 'CloneOption', noTags: false, shallow: true, depth: 1]]
                    ])
                }
            }
        }

        stage('npm install') {
            steps {
                // Build your application here (e.g., compile, package, etc.)
                sh '''
                ls
                pwd
                cd src
                npm install
                echo "In Build Step"
                '''
            }
        }

        stage('npm start') {
            steps {
                // Run your tests (e.g., unit tests, integration tests)
                sh '''
                npm start &
                '''
                echo "this is npm start stage"
            }
        }
    }

    post {
        success {
            // Actions to perform when the pipeline succeeds
            echo 'Pipeline succeeded!'
        }
        failure {
            // Actions to perform when the pipeline fails
            echo 'Pipeline failed!'
        }
    }
}
