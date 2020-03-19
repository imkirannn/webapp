node ('master') {
  stage('Check-Git-Secrets') {
	sh 'rm trufflehog || true'
        sh 'docker run gesellix/trufflehog --json https://github.com/imkirannn/webapp.git > trufflehog'
        sh 'cat trufflehog'
	}
 stage('Clone repository') {
        checkout scm
    }
 stage ('Source Composition Analysis') {
  sh 'npm install' 
	sh 'rm owasp* || true'
         sh 'wget "https://raw.githubusercontent.com/cehkunal/webapp/master/owasp-dependency-check.sh" '
         sh 'chmod +x owasp-dependency-check.sh'
         sh 'bash owasp-dependency-check.sh'
         sh 'cat /var/lib/jenkins/OWASP-Dependency-Check/reports/dependency-check-report.xml'
	}

 stage ('SAST'){
	sh 'sonar-scanner \
  -Dsonar.projectKey=webapp-sast \
  -Dsonar.sources=. \
  -Dsonar.host.url=http://ci-jenkins.cloudhands.online \
  -Dsonar.login=19aecfaf0d879e44785dd65d056507e267a0f31f'

}

stage ('UNIT') {
    catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE'){

  sh 'npm test'

}
}
    stage('Deploy'){
        sh 'npm install'
    }

}
