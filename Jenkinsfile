@Library('Shared')_
pipeline{
    agent { label 'dev-server'}
    
    stages{
        stage("Code clone"){
            steps{
                sh "whoami"
            clone("https://github.com/LondheShubham153/django-notes-app.git","main")
            }
        }
        stage("Code Build"){
            steps{
            dockerbuild("notes-app","latest")
            }
        }
        stage("Push to DockerHub"){
            steps{
                dockerpush("dockerHubCreds","notes-app","latest")
            }
        }
        stage("Deploy"){
            steps{
                deploy()
            }
        }
        stage('Send Email') {
        steps {
        emailext(
            subject: "Jenkins Build ${env.BUILD_NUMBER} - ${currentBuild.currentResult}",
            body: """
                Build Status: ${currentBuild.currentResult}
                Job: ${env.JOB_NAME}
                Build Number: ${env.BUILD_NUMBER}
                Build URL: ${env.BUILD_URL}
            """,
            to: 'roshankhopade5339@gmail.com'
        )
        }
        }
    }
}
