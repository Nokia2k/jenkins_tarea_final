pipeline {
  agent {
    node { 
      label 'nodo'
    }
  }
  stages {
    stage('Descargando archivos') {
      steps {
        sh 'https://github.com/Nokia2k/jenkins_tarea_final.git'
      }
    }
  }
}
