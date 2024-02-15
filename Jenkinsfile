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
        sh 'python3 /home/servidor/workspace/TareaFinal/python-diff.py old.xlsx new.xlsx'
        sh 'pandoc -s meta-logs.md -o meta-logs.pdf --pdf-engine=wkhtmltopdf'
      }  
    }
  }
}
