pipeline {
  agent {
    node { 
      label 'nodo'
    }
  }
  stages {
    stage('Descargando archivos') {
      steps {
        sh 'git clone https://github.com/Nokia2k/jenkins_tarea_final.git'
      }
    }
  }
}
