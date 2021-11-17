pipeline{
    agent any
    tools{
        gradle 'Gradle'
    }
    stages{
        stage('build jar'){
            steps{
                echo "Building war file"
                sh './gradlew clean build'
            }
        }
        stage('build docker image'){
            steps{
                echo "Buildind docker image"
                sh 'docker build -t java-mvn:0.1 .'
            }
        }
        stage('deploy'){
            steps{
                echo "Deploying application"
                sh 'docker rm -f java-gradle-app'
                sh 'docker run --rm -dp 4444:8080 --name java-gradle-app java-mvn:0.1'
                echo "Application is live on <ip-address>:4444"
            }
        }
    }
    post{
        success{
            archiveArtifacts artifacts: 'build/**/*-SNAPSHOT.jar', followSymlinks: false
        }
    }
}
