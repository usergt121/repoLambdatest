#!/usr/bin/env groovy

node {
    withEnv(["LT_USERNAME=testergsr33",
    "LT_ACCESS_KEY=zP2pRMvKbXSwCMNp6d54pcHxEaGpvX6hSsXIdvHzcJyE9O58Cy",
    "LT_TUNNEL=true"]){

    echo env.LT_USERNAME
    echo env.LT_ACCESS_KEY 
    
   stage('setup') { 
   
      // Get some code from a GitHub repository
    try{
      git 'https://github.com/LambdaTest/nightwatch-selenium-sample.git'

      //Download Tunnel Binary
      sh "wget http://downloads.lambdatest.com/tunnel/linux/64bit/LT_Linux.zip"

      //Required if unzip is not installed
      sh 'sudo apt-get install --no-act unzip'
      sh 'unzip -o LT_Linux.zip'

      //Starting Tunnel Process 
      sh "./LT -user ${env.LT_USERNAME} -key ${env.LT_ACCESS_KEY} &"
      sh  "rm -rf LT_Linux.zip"
    }
    catch (err){
      echo err
   }
    
   }
   stage('build') {
      // Installing Dependencies
      sh 'npm install'
    }
   
   stage('test') {
          try{
          sh './node_modules/.bin/nightwatch -e chrome,edge tests'
          }
          catch (err){
          echo err
          }  
   }
   stage('end') {  
     echo "Success" 
     }
 }
}
