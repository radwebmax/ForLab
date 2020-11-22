pipeline{
  options{timestamps()}
  agent none
  stages{
    stage("Check scm"){
      agent any
      steps{
        checkout scm
       }
     }
     stage('Build'){
      steps{
        echo "Building...${BUILD_NUMBER}"
        echo "Build completed"
      }
    }
     stage("Test"){
      agent{docker {image 'alpine'
              args '-u=\"root\"'
              }
            }
       steps{
        script { System.setProperty("Dorg.jenkinsci.plugins.durabletask.BourneShellScript.LAUNCH_DIAGNOSTICS", "true"); }
        //sh 'apk add --update python3 py-pip'
        //sh 'pip install xmlrunner'
        sh 'python3 test.py'
       }
       post{
        always{
          junit "test-reports/*.xml"
            }
        success{
          echo 'Application testing successfully completed'
        failure{
          echo 'F#ck, smth went wrong =('
        }
      }
    }
  }
 }
}
     
      
