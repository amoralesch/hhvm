pipeline {
  agent {
    kubernetes {
      defaultContainer 'maven'
      yaml """
apiVersion: v1
kind: Pod
metadata:
  namespace: dev
spec:
  volumes:
  - name: maven-repo
    persistentVolumeClaim:
      claimName: maven-repo
  containers:
  - name: maven
    image: maven:3-jdk-13-alpine
    volumeMounts:
    - mountPath: "/root/.m2/repository"
      name: maven-repo
    command:
    - cat
    tty: true
"""
    }
  }
  stages {
    stage('maven') {
      steps {
        sh 'mvn clean package'
      }
    }
  }
}