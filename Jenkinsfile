pipeline {
  agent any
  stages {
    stage ('test') {
                steps {
                    bat 'gradle test'
                    archiveArtifacts 'build/test-results/'
                    cucumber reportTitle: 'Cucumber report',
                    fileIncludePattern: 'target/report.json',
                    trendsLimit: 10,
                    classifications: [
                        [
                           'key': 'Browser',
                            'value': 'Firefox'
                        ]
                    ]
                    junit 'build/test-results/test/TEST-Matrix.xml'
                }
             }
}

}