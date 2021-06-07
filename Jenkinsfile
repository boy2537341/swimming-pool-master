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
            environment {
                SONAR_TOKEN = credentials('user02_SonarQube')
            }
            steps {
                sh './gradlew sonarqube \
                  -Dsonar.projectKey=swimming-pool-user02 \
                  -Dsonar.host.url=http://140.134.26.54:10990 \
                  -Dsonar.login=ca92f0e583e29f93dbb46ffdd347a9cb7a216fdf'
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
    }
}
