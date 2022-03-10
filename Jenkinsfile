pipeline {
    parameters {
      string defaultValue: 'main', description: 'The branch to checkout (default: main)', name: 'BRANCH'
    }

    agent any
    
    tools {
      maven "mvn3.8.4"
    }

    stages {
      stage('Build stage') {
        steps {
            echo 'Building ${BRANCH} branch'
            sh 'mvn clean install'
        }
      }

      stage('Test stage') {
	when {
	   expression { BRANCH == "master" }
	}
       agent {
        label 'built-in'
       }

       steps {
        sh 'mvn test'
       }
    }


    stage('Clean Workspace') {
      steps {
        cleanWs()
      }
    }
  }
}
