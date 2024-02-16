pipeline {
  agent {
    node { 
      label 'nodo'
    }
  }
  stages {
    stage('Ejecutanto el scritpt') {
      steps {
        sh 'chmod 764 /home/servidor/workspace/TareaFinal/python-diff.py'
        sh 'python3 /home/servidor/workspace/TareaFinal/python-diff.py old.xlsx new.xlsx'
        // EN ESTE PASO NOTIFICAR VIA TELEGRAM SI TODO HA IDO BIEN
      }  
    }
    stage('Enviar y ejecutar el meta-script') {
      steps {
        sh 'scp -p meta-script.sh admin@172.17.0.4:/home/admin/meta-script.sh'
        sh 'ssh admin@172.17.0.4 ./hu.sh'
        // AQUI TIENE QUE HABER UN BOT QUE NOTIFIQUE POR TELEGRAM
      }
    } 
    stage('Enviar el md a github') {
      steps {
        sh 'git config --global user.email \'vicmarmartinezmartinez@gmail.com\''
        sh 'git config --global user.name \'Nokia2k\''
        sh 'git add meta-logs.md';
        sh 'git commit -m "logs subidos"';
        withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
          sh('git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/Nokia2k/jenkins_tarea_final.git HEAD:main')
        }
      }
    }
    stage('Generando el pdf con pandoc'){
      steps {
        sh 'pandoc -s meta-logs.md -o meta-logs.pdf --pdf-engine=wkhtmltopdf'
      }
    }
    stage('envio de un correo de notificacion de la ejecucion') {
      steps {
        sh 'echo aqui nose como enviarlo por correo'
      }
    } 
  }
}
