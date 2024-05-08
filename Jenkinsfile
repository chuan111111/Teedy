pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('pmd') {
            steps {
                sh 'mvn pmd:pmd'
            }
        }
         stage('Doc') {
            steps {
                sh 'mvn javadoc:jar'
            }
        }
        stage('Test report') {
            steps {
                sh 'mvn -Dtest=TestAclResource test --fail-never'
            }
        }
    }
    
    post {
        always {
            archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/pmd.html', fingerprint: true
            archiveArtifacts artifacts: '**/target/surefire-reports/*xml', fingerprint: true
        }
    }
    
}
