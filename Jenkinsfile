pipeline{
    triggers { upstream(upstreamProjects: 'fastapi-cicd', threshold: hudson.model.Result.SUCCESS) }
    agent {
        docker {
            image "postman/newman"
            args "--entrypoint=''"
        }   
    }

    stages{
        stage('Test API et génération de rapport'){
            steps{
                sh 'newman run collections/collection.json -r cli,junit --reporter-junit-export="newman-report.xml"'
            }
        }
    }

    post{
        always {
            junit 'newman-report.xml'
        }
    }
}
