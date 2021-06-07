pipeline {
    agent any
    /* insert Declarative Pipeline here */
    stages {
        stage('run-test') {
            /* when {
                anyOf {
                    branch 'master'
                    branch 'dev'
                }
            } */
            steps {
                sh 'chmod +x ./gradlew'
                sh './gradlew test'
                jacoco(
                    classPattern: 'app/build/classes',
                    inclusionPattern: '**/*.class',
                    exclusionPattern: '**/*Test*.class',
                    execPattern: 'app/build/jacoco/**/*.exec'
                )
            }
        }
        stage('sonarqube-analysis') {
            environment {
                SONAR_TOKEN = credentials('team1_swimming-pool_user02')
            }
            steps {
                sh '''./gradlew sonarqube \
                      -Dsonar.projectKey=swimming-pool-user02 \
                      -Dsonar.host.url=http://140.134.26.54:10990 \
                      -Dsonar.login=7d5a0502dbb0ad164e977bca1873356ae8e41432
                '''
            }
        }
    }
}
