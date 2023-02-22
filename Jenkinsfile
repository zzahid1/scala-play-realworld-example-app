// Uses Declarative syntax to run commands inside a container.
pipeline {
    agent {
        kubernetes {
            // Rather than inline YAML, in a multibranch Pipeline you could use: yamlFile 'jenkins-pod.yaml'
            // Or, to avoid YAML:
            // containerTemplate {
            //     name 'shell'
            //     image 'ubuntu'
            //     command 'sleep'
            //     args 'infinity'
            // }
/*             yaml '''
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: shell
    image: ubuntu
    command:
    - sleep
    args:
    - infinity
''' */
            // Can also wrap individual steps:
            // container('shell') {
            //     sh 'hostname'
            // }
         //   defaultContainer 'shell'
        }
    }
    stages {
        stage('java install'){
            steps('build'){
                //sh "sudo apt update -y && sudo apt install -y default-jdk"
                sh "echo hello"
            }
        }
        stage('SonarQube Analysis') {
            //def scannerHome = tool 'SonarScanner';
            steps('build 2'){
                withSonarQubeEnv('sonarqube') {
                    sh "sbt sonarScan"
                }
            }
  }
    }
}