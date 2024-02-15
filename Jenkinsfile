pipeline {
  agent any
  stages {
    stage('Descargando archivos') {
      steps {
        sh 'https://github.com/Nokia2k/jenkins_tarea_final.git'
      }
    }
    stage('Genereando script .sh') {
      steps {
        sh 'cp /var/jenkins_home/workspace/TareaFinal/index /var/www/index.html'
      }
    }

  }
}
