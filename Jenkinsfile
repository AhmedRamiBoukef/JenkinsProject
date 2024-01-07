pipeline {
  agent any
  stages {
    stage ('test') {
                steps {
                    bat 'gradlew.bat test'
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
          stage ('Code Analysis') {
                      steps {
                                          withSonarQubeEnv('sonar'){
                          bat 'gradlew.bat sonarqube'
                                          }
                      }
                   }
             stage("Quality gate") {
                         steps {
                             waitForQualityGate abortPipeline: true
                         }
                     }

              stage("Build") {
                         steps {
                             bat 'gradlew.bat build'
                             bat 'gradlew.bat javadoc'
                             archiveArtifacts 'build/libs/*.jar'
                             archiveArtifacts 'build/docs/'
                         }
                     }
              stage("deploy") {
                         steps {
                             bat 'gradlew.bat publish'

                         }
                     }
}

}