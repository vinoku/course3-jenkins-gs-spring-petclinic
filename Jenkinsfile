pipeline {
    agent any

    stages {
        stage("Build") {
            steps {
                bat 'mvnw.cmd package'
            }
        }

        stage("Capture") {
           steps {
                archiveArtifacts '**/target/*.jar'
                jacoco()
                junit '**/target/surefire-reports/TEST*.xml'
           }
        }
    }

    post {
        always {
            emailext body: "${env.BUILD_URL}\n${currentBuild.absoluteUrl}",
                to: "always@foo.bar",
                recipientProviders: [previous()],
                subject: "${currentBuild.currentResult}: Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]"
        }
    }

}
