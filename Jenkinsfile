pipeline {
    agent any
    environment {
        imagename = "himan14/docker-jenkins"
        registryCredential = 'dockerhub'
        dockerImage = ''
    }
    stages {
        stage("Cloning Git") {
            steps {
                echo "========executing Cloning Stage========"
                git ([url: 'https://github.com/CunningLearner/docker-demo.git', branch: 'master'])
            }
            post{
                always{
                    echo "========always========"
                }
                success{
                    echo "========Cloning executed successfully========"
                }
                failure{
                    echo "========Cloning execution failed========"
                }
            }
        }
        stage('Building Image') {
            steps {
                script {
                    dockerImage = docker.build imagename
                }
            }
            post{
                always{
                    echo "========always========"
                }
                success{
                    echo "========Building executed successfully========"
                }
                failure{
                    echo "========Building execution failed========"
                }
            }
        }
        stage('Deploy Image') {
            steps {
                script {
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push($BUILD_NUMBER)
                        dockerImage.push(latest)
                    }
                }
            }
            post{
                always{
                    echo "========always========"
                }
                success{
                    echo "========Deploy executed successfully========"
                }
                failure{
                    echo "========Deploy execution failed========"
                }
            }
        }
    }

}