pipeline {

    agent {
      label "WaveMaker HyScale Pipeline Demo"
  }
  
  tools {
    jdk "jdk8"
    maven "mvn3.3.8"
  }
  
  environment {
	BUILD_NUMBER=10
  }
  
  stages {
    stage("QA") {
      steps {
        timeout(time: true, uint: 'MINUTES') {
          echo "We're not doing anything particularly special here."
          echo "Just making sure that we don't take longer than five minutes"
          echo "Which, I guess, is kind of silly."
          sh "mvn -version" 
        }
      }
      post {
        success {
          echo "Only when we haven't failed running the first stage"
        }
        
        failure {
          echo "Only when we fail running the first stage."
        }
      }
    }
    
    stage('STAGE') {
      tools {
        maven "mvn3.3.9"
      }
      
      steps {
        echo "This time, the Maven version should be 3.3.9"
        sh "mvn -version"
      }
    }
    
    stage('LIVE') {
      steps {
        parallel(one: {
                  echo "I'm on the first branch!"
                 },
                 two: {
                   echo "I'm on the second branch!"
                 },
                 three: {
                   echo "I'm on the third branch!"
                   echo "But you probably guessed that already."
                 })
      }
    }
  }
  
  post {
    // Always runs. And it runs before any of the other post conditions.
    always {
      // Let's wipe out the workspace before we finish!
      deleteDir()
    }
    
    success {
      mail(from: "bob@example.com", 
           to: "steve@example.com", 
           subject: "That build passed.",
           body: "Nothing to see here")
    }

    failure {
      mail(from: "bob@example.com", 
           to: "steve@example.com", 
           subject: "That build failed!", 
           body: "Nothing to see here")
    }
  }
    timeout(time: 60, unit: 'MINUTES')
  }

}
