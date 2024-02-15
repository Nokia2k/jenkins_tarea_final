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
        ## EN ESTE PASO NOTIFICAR VIA TELEGRAM SI TODO HA IDO BIEN
      }  
    }
    stage('Enviar y ejecutar el meta-script') {
      steps {
        ## AQUI HAY QUE GENERAR UN PAR DE CLAVES PUBLICAS PARA QUE NO PREGUNTE POR LA CONTRASEÑA
        #sh 'scp -p meta-script.sh admin@172.17.0.XXX:/usr/bin/meta-script.sh'
        #sh 'ssh admin@172.17.0.XXX meta-script.sh'
        ## AQUI TIENE QUE HABER UN BOT QUE NOTIFIQUE POR TELEGRAM
      }
    } 
    stage('Enviar el md a github') {
      steps {
        sh 'echo aqui haria el push'
      }
    }
    stage('Generando el pdf con pandoc'){
      steps {
        sh 'pandoc -s meta-logs.md -o meta-logs.pdf --pdf-engine=wkhtmltopdf'
      }
    stage('envio de un correo de notificacion de la ejecucion') {
      steps {
        sh 'echo aqui nose como enviarlo por correo'
      }
    } 
  }
}
