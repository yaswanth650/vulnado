pipeline {
    agent any
    tools {
    maven 'Maven'
  }
   stages {
    stage('CodeQLAnalysis') {
            steps {
                withCodeQL(codeql: 'codeql') {
                    sh 'codeql database create my-database --language=java --source-root=. --overwrite '
                    sh 'codeql database analyze my-database --format=sarifv2.1.0 --output=results.sarif'
                }
            }
        post {
        always {
            archiveArtifacts artifacts: 'results.sarif', allowEmptyArchive: true
            recordIssues tools: [sarif(pattern: 'results.sarif')]
        }
       }
    }
    stage('CodeQL-Analysis') {
            steps {
                withCodeQL(codeql: 'codeql') {
                    sh 'codeql database create my-database --language=java --source-root=. --overwrite '
                    sh 'codeql database analyze my-database --format=csv --output=results.csv'
                }
            }
        post {
        always {
            archiveArtifacts artifacts: 'results.csv', allowEmptyArchive: true
        }
       }
    }
    stage('CODEQLANALYSIS') {
            steps {
                withCodeQL(codeql: 'codeql') {
                    sh 'codeql database create my-database --language=java --source-root=. --overwrite '
                    sh 'codeql database analyze my-database --format=sarif-latest --output=results1.sarif'
                }
            }
        post {
        always {
            archiveArtifacts artifacts: 'results1.sarif', allowEmptyArchive: true
            recordIssues tools: [sarif(pattern: 'results1.sarif')]
        }
       }
    }
    }
}
