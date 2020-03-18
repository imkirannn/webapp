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
	sh 'rm owasp* || true'
         sh 'wget "https://raw.githubusercontent.com/cehkunal/webapp/master/owasp-dependency-check.sh" '
         sh 'chmod +x owasp-dependency-check.sh'
         sh 'bash owasp-dependency-check.sh'
         sh 'cat /var/lib/jenkins/OWASP-Dependency-Check/reports/dependency-check-report.xml'
	}

