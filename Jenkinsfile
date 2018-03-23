#!groovy

/*

###########################################################################

Change History
Date            Author              Description
##########      ###############     #######################################
05/12/2017      charles.lambert     Original creation
08/29/2017      charles.lambert     adjust for containerized app
01/12/2018      Rakesh Panakkal     Modified for 3PO BE
01/18/2018      charles.lambert     Match dir struc
###########################################################################
*/

def version() {
  def matcher = readFile('pom.xml') =~ '<version>(.+)</version>'
  matcher ? matcher[0][1] : null
}

def artifactId() {
  def matcher = readFile('pom.xml') =~ '<artifactId>.+)</artifactId>'
  matcher ? matcher[0][1] : null
}

node('java8') {

  /*
    USER INPUT variables
    // User defined Env variables
    // Must be updated as required.

    */
    /*###########################################################################*/
    /*###########################################################################*/
    
    
    
    currentBuild.result = "SUCCESS"
    env.NODE_ENV = "dev"
    env.PROJECT = "hello-world"
	env.VERSION = "0.1"
    /*###########################################################################*/
    /*###########################################################################*/


    try {

        stage('Build and Pubish Container'){
      
            sh "sudo docker login -u Containerakalya -p 2Xf/vzHX0X1tXDd0TnMppa9w98thkVrd containerakalya.azurecr.io"
            sh "sudo docker build . -t containerakalya.azurecr.io/${env.PROJECT}/${env.NODE_ENV}:${env.VERSION}"
            sh "sudo docker push containerakalya.azurecr.io/${env.PROJECT}/${env.NODE_ENV}:${env.VERSION}"
                   
         }


       }

      catch (err) {

      currentBuild.result = "FAILED"
      bitbucketStatusNotify ( buildState: 'FAILED' )
      
      if (err) {
        timestamps {
          throw err
        }
      }
    }
}