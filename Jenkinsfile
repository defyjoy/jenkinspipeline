pipeline {
  agent {
    kubernetes {
      yaml '''
        apiVersion: v1
        kind: Pod
        metadata:
          labels:
            some-label: some-label-value
        spec:
          containers:
          - name: maven
            image: maven:alpine
            command:
            - cat
            tty: true
          - name: busybox
            image: busybox
            command:
            - cat
            tty: true
        '''
      retries 2
    }
  }
  stages {
    stage('Run maven') {
      steps {
        container('maven') {
        //   sh 'mvn -version'
            sh "echo hello world"
        }
        container('busybox') {
          sh "echo hello world"
        }
      }
    }
  }
}


// podTemplate(containers: [
//     containerTemplate(name: 'maven', image: 'maven:3.3.9-jdk-8-alpine', ttyEnabled: true, command: 'cat'),
//     containerTemplate(name: 'golang', image: 'golang:1.8.0', ttyEnabled: true, command: 'cat')
//   ]) {

//     node(POD_LABEL) {
//         stage('Get a Maven project') {
//             git 'https://github.com/jenkinsci/kubernetes-plugin.git'
//             container('maven') {
//                 stage('Build a Maven project') {
//                     sh """
//                     echo hello world
//                     """
//                 }
//             }
//         }

//         stage('Get a Golang project') {
//             git url: 'https://github.com/hashicorp/terraform.git'
//             container('golang') {
//                 stage('Build a Go project') {
//                     sh """
//                     echo hello world
//                     """
//                 }
//             }
//         }

//     }
// }