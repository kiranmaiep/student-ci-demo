pipeline {
  agent any
  options { timestamps(); timeout(time: 15, unit: 'MINUTES') }

  stages {
    stage('Checkout') {
      steps { checkout scm }
    }

    stage('Build') {
      steps {
        bat """
        if exist out rmdir /s /q out
        mkdir out
        javac -d out src\\hello\\Hello.java
        """
      }
    }

    stage('Run') {
      steps {
        bat """
        java -cp out hello.Hello
        echo Build_OK > artifact.txt
        """
      }
    }
  }

  post {
    always {
      archiveArtifacts artifacts: 'artifact.txt, out/**', allowEmptyArchive: false
    }
  }
}
