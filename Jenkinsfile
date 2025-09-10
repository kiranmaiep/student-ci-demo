pipeline {
  agent any
  options { timestamps(); timeout(time: 15, unit: 'MINUTES') }
  stages {
    stage('Checkout'){ steps { checkout scm } }
    stage('Build'){
      steps {
        bash -lc 'rm -rf out && mkdir -p out && javac -d out src/hello/Hello.java'
      }
    }
    stage('Run'){
      steps { bash -lc 'java -cp out hello.Hello' }
    }
  }
  post { always { archiveArtifacts artifacts: 'out/**', allowEmptyArchive: false } }
}
