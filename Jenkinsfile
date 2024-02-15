pipeline {
  agent {
    node { 
      label 'nodo'
    }
  }
  stages {
    stage('Generando meta-script') {
      steps {
        sh 'chmod 764 /home/servidor/workspace/TareaFinal/python-diff.py'
        sh 'bash /home/servidor/workspace/TareaFinal/python-diff.py users-240122.xlsx users-240123.xlsx'
      }  
    }
  }
}
