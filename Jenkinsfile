pipeline {
  agent any

  tools {
    maven 'M3'
    jdk 'JDK21'
  }
  stages {
    //GitHub Clone
    stage('Git Clone') {
      steps {
        git url: 'https://github.com/dmsqlsS2/spring-petclinic.git', branch: 'main'
      }
    }

    //Maven Build
    stage('Maven Build') {
      steps {
        sh 'mvn -Dmaven.test.failure.ignore=true clean package'
      }
    }

    //Docker Image 생성
    stage('Docker Image Build') {
      steps {
        dir("${env.WORKSPACE}") {
          sh """
          docker build -t dmsqls/spring-petclinic:$BUILD_NUMBER .
          docker tag dmsqls/spring-petclinic:$BUILD_NUMBER dmsqls/spring-petclinic:latest
          """
        
        }
        
      }
    }
    
  }
}
