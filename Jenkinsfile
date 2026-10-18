pipeline {
    agent any

    stages {
        stage('Code checkout') {
            steps {
                echo 'Cloning the code'
                git branch: 'main',
                    url: 'https://github.com/Vikas-525/DevopsProject1.git'
            }
        }

        stage('Maven unit Test') {
            steps {
                dir('/var/lib/jenkins/workspace/project1') {
                    sh 'mvn test'
                }
            }
        }

        stage('Maven Build') {
            steps {
                dir('/var/lib/jenkins/workspace/project1') {
                    sh 'mvn clean install'
                }
            }
        }

        stage('Maven Integration Test') {
            steps {
                dir('/var/lib/jenkins/workspace/project1') {
                    sh 'mvn verify'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building docker image'
                sh 'docker build -t ci-pipeline .'
            }
        }

        stage('Push image to dockerhub') {
            steps {
                echo 'Pushing image to DockerHub'

                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerHub',
                        usernameVariable: 'dockerHubUser',
                        passwordVariable: 'dockerHubPass'
                    )
                ]) {
                    sh '''
                        docker tag ci-pipeline "$dockerHubUser/ci-pipeline:latest"

                        echo "$dockerHubPass" | docker login \
                            -u "$dockerHubUser" --password-stdin

                        docker push "$dockerHubUser/ci-pipeline:latest"
                    '''
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps{
                dir('/var/lib/jenkins/workspace/project1') {
                    withKubeConfig(
                        credentialsId: 'kubernetes',
                        restrictKubeConfigAccess: false
                    ) {
                        sh '''
                            kubectl apply -f deployment.yaml
                            kubectl apply -f service.yaml
                        '''
                    }
                 }
            }
        }
    }
}
