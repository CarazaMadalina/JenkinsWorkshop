pipeline {
    parameters {
      string defaultValue: 'master', description: 'The branch to checkout (default: master)', name: 'BRANCH'
    }

    agent any
    
    tools {
      maven "mvn3.8.4"
    }

    stages {
      stage('Build stage') {
        steps {
            sh 'echo Building ${BRANCH} branch'
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
