pipeline {
   agent none
   environment {
       LAST = 'not_set'
   }
   options { 
      skipStagesAfterUnstable()
   }
   stages {
        stage('build GitHub') {
            // agent - uses jenkins master 
            steps{
                echo 'Everybody says Hi'
                //input "please hit any key ..."
            }
        }
        
        stage('maven example') {
            agent {
                docker {
                    image 'maven:3.3.3'
                }
            }
            steps{
                retry(3) {                  // on fail
                    sh 'mvn --version'
                }
                timeout(time: 3, unit: 'MINUTES') {
                    sh 'mvn --version'   
                }
            }
        }
        
        stage('python example') {
            agent {
                docker {
                    image 'python'
                }
            }
            steps{
                sh 'python --version'
                // sh 'python --version-fail'

            }
        }  
        
        stage('node example') {
            agent {
                docker {
                    image 'node'
                }
            }
            steps{
                sh 'node --version'
            }
        }  
   }
   post {
       always {
           echo 'always / finally example'
           // deleteDir()                       // clean-up
           // junit 'build/reports/**/*.xml'
           // achiveArtifacts artifacts: 'build/libs/**/*.jar', fingerprint: true 
       }
       success {
           echo 'success example'
           //echo "${LAST}"
       }
       failure{
            echo 'failure example'
            //echo "${LAST}"
       }
       unstable {
          // non-blocking failure
           echo 'unstable example'
           
       }
       changed {
           // compares any change to last/previous build status
            echo 'changed example'
       }
   }

}
