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
        sh 'curl -X POST -H \'Content-Type: application/json\' -d \'{"chat_id": "1377996077", "text": "Paso 1 funciona", "disable_notification": false}\'  https://api.telegram.org/bot6639961602:AAFcMakUo0Q7oSCTBocZYCd6IfMWm14xFPk/sendMessage'
      }  
    }
    stage('Enviar y ejecutar el meta-script') {
      steps {
        sh 'scp -p meta-script.sh admin@172.17.0.4:/home/admin/meta-script.sh'
        sh 'ssh admin@172.17.0.4 ./hu.sh'
        sh 'curl -X POST -H \'Content-Type: application/json\' -d \'{"chat_id": "1377996077", "text": "Paso 2 funciona", "disable_notification": false}\'  https://api.telegram.org/bot6639961602:AAFcMakUo0Q7oSCTBocZYCd6IfMWm14xFPk/sendMessage'
      }
    } 
    stage('Enviar el md a github') {
      steps {
        sh 'git config --global user.email \'vicmarmartinezmartinez@gmail.com\''
        sh 'git config --global user.name \'Nokia2k\''
        sh 'git add meta-logs.md';
        sh 'git commit -m "subidos" --force';
        withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
          sh('git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/Nokia2k/jenkins_tarea_final.git HEAD:main')
        }
        sh 'curl -X POST -H \'Content-Type: application/json\' -d \'{"chat_id": "1377996077", "text": "Paso 3 funciona", "disable_notification": false}\'  https://api.telegram.org/bot6639961602:AAFcMakUo0Q7oSCTBocZYCd6IfMWm14xFPk/sendMessage'

      }
    }
    stage('Generando el pdf con pandoc'){
      steps {
        sh 'pandoc -s meta-logs.md -o meta-logs.pdf --pdf-engine=wkhtmltopdf'
        sh 'curl -X POST -H \'Content-Type: application/json\' -d \'{"chat_id": "1377996077", "text": "Generar pdf funciona", "disable_notification": false}\'  https://api.telegram.org/bot6639961602:AAFcMakUo0Q7oSCTBocZYCd6IfMWm14xFPk/sendMessage'
      }
    }
    stage('envio de un correo de notificacion de la ejecucion') {
      steps {
        sh 'echo aqui nose como enviarlo por correo'
      }
    } 
  }
}
