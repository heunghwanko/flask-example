node {
     stage('Clone repository') {
         checkout scm
     }
     stage('Build image') {
         app = docker.build("admin/flask-example")
         
     }
     stage('Push image') {
         docker.withRegistry('https://127.0.0.1/', 'harbor_cred') {
             app.push("${env.BUILD_NUMBER}")
             app.push("latest")
         }
     stage('SonarQubeScanner') {
         def scannerHome = tool 'SonarQubeScanner';
         withSonarQubeEnv('SonarQubeScanner') {
             sh """${scannerHome}/bin/sonar-scanner \
                             -Dsonar.projectKey=demo-project \
                             -Dsonar.sources=. \
                             -Dsonar.host.url=http://10.0.2.15:9000 \
                             -Dsonar.login=squ_ae550991b03cff5011b1b33d51c8a915bc373059
             """
        }
     }
     
}
