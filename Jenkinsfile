#!groovy

node {
   // ------------------------------------
   // -- ETAPA: Compilar
   // ------------------------------------
   stage 'Compilar'
   
   // -- Configura variables
   echo 'Configurando variables'
   def mvnHome = tool 'M3'
   env.PATH = "${mvnHome}/bin:${env.PATH}"
   echo "var mvnHome='${mvnHome}'"
   echo "var env.PATH='${env.PATH}'"
   
   // -- Descarga código desde SCM
   echo 'Descargando código de SCM'
   sh 'rm -rf *'
   checkout scm
   
   // -- Compilando
   echo 'Compilando aplicación'
   sh 'mvn clean compile'

stage ('Static code analysis') {
    sh "sudo phpcs --config-set ignore_warnings_on_exit 1 --report=checkstyle --report-file=checkstyle-result.xml -q /code"
    step([$class: 'hudson.plugins.checkstyle.CheckStylePublisher', pattern: 'checkstyle-*'])
}
   
   
}
