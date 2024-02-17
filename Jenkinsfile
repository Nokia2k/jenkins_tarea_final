pipeline {
  agent {
    node { 
      label 'nodo'
    }
  }
  stages {
    stage('Ejecutanto el scritpt') {
      steps {
        sh 'curl -X POST -H \'Content-Type: application/json\' -d \'{"chat_id": "1377996077", "text": "___", "disable_notification": false}\'  https://api.telegram.org/bot6639961602:AAFcMakUo0Q7oSCTBocZYCd6IfMWm14xFPk/sendMessage'
        sh 'curl -X POST -H \'Content-Type: application/json\' -d \'{"chat_id": "1377996077", "text": " * Ejecucion de la Tarea:", "disable_notification": false}\'  https://api.telegram.org/bot6639961602:AAFcMakUo0Q7oSCTBocZYCd6IfMWm14xFPk/sendMessage'
        sh 'chmod 764 /home/servidor/workspace/TareaFinal/python-diff.py'
        sh 'python3 /home/servidor/workspace/TareaFinal/python-diff.py old.xlsx new.xlsx'
        sh 'chmod 764 /home/servidor/workspace/TareaFinal/meta-script.sh'
        sh 'curl -X POST -H \'Content-Type: application/json\' -d \'{"chat_id": "1377996077", "text": "Paso 1: Ejecutando el script. -> Correcto.", "disable_notification": false}\'  https://api.telegram.org/bot6639961602:AAFcMakUo0Q7oSCTBocZYCd6IfMWm14xFPk/sendMessage'
      }  
    }
    stage('Enviar y ejecutar el meta-script') {
      steps {
        sh 'scp -p meta-script.sh admin@172.17.0.4:/home/admin/meta-script.sh'
        sh 'ssh -S admin@172.17.0.4 sudo ./meta-script.sh'
        sh 'curl -X POST -H \'Content-Type: application/json\' -d \'{"chat_id": "1377996077", "text": "Paso 2: Enviar y ejecutar el meta-script. -> Correcto.", "disable_notification": false}\'  https://api.telegram.org/bot6639961602:AAFcMakUo0Q7oSCTBocZYCd6IfMWm14xFPk/sendMessage'
      }
    } 
    stage('Generando el pdf con pandoc'){
      steps {
        sh 'pandoc -s meta-logs.md -o meta-logs.pdf --pdf-engine=wkhtmltopdf'
        sh 'curl -X POST -H \'Content-Type: application/json\' -d \'{"chat_id": "1377996077", "text": "Paso 3: Generando el pdf. -> Correcto", "disable_notification": false}\'  https://api.telegram.org/bot6639961602:AAFcMakUo0Q7oSCTBocZYCd6IfMWm14xFPk/sendMessage'
        sh 'curl -X POST -H \'Content-Type: application/json\' -d \'{"chat_id": "1377996077", "text": " * Compartiendo documento PDF:", "disable_notification": false}\'  https://api.telegram.org/bot6639961602:AAFcMakUo0Q7oSCTBocZYCd6IfMWm14xFPk/sendMessage'
        sh 'curl -X POST "https://api.telegram.org/bot6639961602:AAFcMakUo0Q7oSCTBocZYCd6IfMWm14xFPk/sendDocument" -F chat_id="1377996077" -F document="@meta-logs.pdf"'
      }
    }
    stage('Enviar el md a github') {
      steps {
        sh 'git config --global user.email \'vicmarmartinezmartinez@gmail.com\''
        sh 'git config --global user.name \'Nokia2k\''
        sh 'git add meta-logs.pdf';
        sh 'git commit -m "subidos"';
        withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
          sh('git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/Nokia2k/jenkins_tarea_final.git HEAD:main')
        }
        sh 'curl -X POST -H \'Content-Type: application/json\' -d \'{"chat_id": "1377996077", "text": "Paso 4: Enviar el md a github. -> Correcto", "disable_notification": false}\'  https://api.telegram.org/bot6639961602:AAFcMakUo0Q7oSCTBocZYCd6IfMWm14xFPk/sendMessage'
        sh 'curl -X POST -H \'Content-Type: application/json\' -d \'{"chat_id": "1377996077", "text": " * Compartiendo plantilla MarkDown:", "disable_notification": false}\'  https://api.telegram.org/bot6639961602:AAFcMakUo0Q7oSCTBocZYCd6IfMWm14xFPk/sendMessage'
        sh 'curl -X POST "https://api.telegram.org/bot6639961602:AAFcMakUo0Q7oSCTBocZYCd6IfMWm14xFPk/sendDocument" -F chat_id="1377996077" -F document="@meta-logs.md"'

      }
    }
  }
  post {
    success {
      script {
        sh 'curl -X POST -H \'Content-Type: application/json\' -d \'{"chat_id": "1377996077", "text": " * Tarea terminada con exito", "disable_notification": false}\' https://api.telegram.org/bot6639961602:AAFcMakUo0Q7oSCTBocZYCd6IfMWm14xFPk/sendMessage'
      }
    }
    failure {
      sh 'ssh jenkins@172.17.0.2 zip -r archivos_log.zip ${JENKINS_HOME}/jobs/${JOB_NAME}/builds/${BUILD_NUMBER}'
      sh 'scp jenkins@172.17.0.2:/var/jenkins_home/archivos_log.zip .'
      sh 'curl -X POST -H \'Content-Type: application/json\' -d \'{"chat_id": "1377996077", "text": " * Tarea terminada erroneamente", "disable_notification": false}\' https://api.telegram.org/bot6639961602:AAFcMakUo0Q7oSCTBocZYCd6IfMWm14xFPk/sendMessage'
      sh 'curl -X POST -H \'Content-Type: application/json\' -d \'{"chat_id": "1377996077", "text": " * Compartiendo comprimido con logs:", "disable_notification": false}\' https://api.telegram.org/bot6639961602:AAFcMakUo0Q7oSCTBocZYCd6IfMWm14xFPk/sendMessage'
      sh 'curl -X POST "https://api.telegram.org/bot6639961602:AAFcMakUo0Q7oSCTBocZYCd6IfMWm14xFPk/sendDocument" -F chat_id="1377996077" -F document="@archivos_log.zip"'  
    }
  }
}
