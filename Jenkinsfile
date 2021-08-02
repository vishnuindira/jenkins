pipeline {
    agent any

    stages {
        stage('Anchor scan') {
            steps {
                echo 'Pulling images..'
                echo 'Scanning..'
                echo 'Creating report..'
            }                       
        }
        stage('Helm deploy') {
            steps {
                echo 'Matching the branch..'
                echo 'Checkout..'
                echo 'Helm deployment..'
            }
        }
        stage('Sanity check') {
            steps {
                echo "checking end points"
            }         
        }        
        stage('Workflow posting') {
            steps {
                echo 'Matching the branch..'
                echo 'Checkout..'                
                echo "checking end points"
            }         
        }          
        stage('Testing') {
            steps {
                echo "checking end points"
                echo "running test cases"
            }         
        } 
        stage('Test report') {
            steps {
                echo "checking end points"
                echo "running test cases"
            }         
        }   
        stage('Release') {
            steps {
                echo "Copying helm charts"
                echo "Copying workflows"
                echo "Copying Docs"
            }         
        }         

    }
    environment {
        EMAIL_TO = 'vishnuprasad.vv@quest-global.com'
    }
    
    post {
        success {
            emailext body: 'Check console output at $BUILD_URL to view the results. \n\n ${CHANGES} \n\n -------------------------------------------------- \n${BUILD_LOG, maxLines=100, escapeHtml=false}', 
                    to: "${EMAIL_TO}", 
                    subject: 'Build success in Jenkins: $PROJECT_NAME - #$BUILD_NUMBER'
        }        
        failure {
            emailext body: 'Check console output at $BUILD_URL to view the results. \n\n ${CHANGES} \n\n -------------------------------------------------- \n${BUILD_LOG, maxLines=100, escapeHtml=false}', 
                    to: "${EMAIL_TO}", 
                    subject: 'Build failed in Jenkins: $PROJECT_NAME - #$BUILD_NUMBER'
        }
        unstable {
            emailext body: 'Check console output at $BUILD_URL to view the results. \n\n ${CHANGES} \n\n -------------------------------------------------- \n${BUILD_LOG, maxLines=100, escapeHtml=false}', 
                    to: "${EMAIL_TO}", 
                    subject: 'Unstable build in Jenkins: $PROJECT_NAME - #$BUILD_NUMBER'
        }
        changed {
            emailext body: 'Check console output at $BUILD_URL to view the results.', 
                    to: "${EMAIL_TO}", 
                    subject: 'Jenkins build is back to normal: $PROJECT_NAME - #$BUILD_NUMBER'
        }
    }    
}
