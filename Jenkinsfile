pipeline {
    agent any
    triggers {
        githubPush()
    }
    options {
        timestamps()
    }
    stages {
        stage('Github Repository Clone & Checkout') {
            steps {
                git branch: 'docker',
                    url: 'https://github.com/devlukej/jenkins-cicd.git',
                    credentialsId: 'jenkins'
            }
        }
        stage('Docker Build') {
            steps {
                script{
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-hub') {
                        // Dockerfile로 이미지 생성
                        docker.build('jochanho/jenkins-test', './docker')
                        // docker build -t <계정명>/<리포지토리명|이미지명>:<태그|버전>
                    }
                }
            }
        }
        stage('dockerfile_example') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/devlukej/dockerfile_example.git',
                    credentialsId: 'test'
            }
        }
        stage('apache2 Build') {
            steps {
                script{
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-hub') {
                        docker.build('jochanho/lb_apache2', './ubuntu_apache2')
                    }
                }
            }
        }
                stage('nginx Build') {
            steps {
                script{
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-hub') {
                        docker.build('jochanho/lb_apache2', './ubuntu_nginx')
                    }
                }
            }
        }
        stage('LB Build') {
            steps {
                script{
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-hub') {
                        docker.build('jochanho/lb_apache2', './ubuntu_nginx_loadbalancer')
                    }
                }
            }
        }
        stage('Docker Image Push'){
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-hub') {
                    def img = docker.image('jochanho/jenkins-test')
                    img.push('latest')
                    img.push('0.1')
                    }
                }
            }
        }
    }
    
    post{
        cleanup {
            emailext subject: '[$JOB_NAME - $BUILD_DISPLAY_NAME] - 작업 결과',
            to: 'cici11x55@gmail.com', //받는사람
            body: '$JOB_NAME\n\n작업이 수행되었습니다.\n\n$BUILD_URL \n\n$DEFAULT_CONTENT'
            // cleanWs() //작업영역 삭제
        }
    }
}