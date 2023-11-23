pipeline {
    agent any

    stages {
        stage ('SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/pythoncpp/jenkins-html-demo.git'
            }
        }
        stage ('docker login') {
            steps {
                sh 'echo dckr_pat_CRWs629s1SidfG9UTpe-nqQoUSM | /usr/local/bin/docker login -u pythoncpp --password-stdin'
            }
        }
        stage ('docker build image') {
            steps {
                sh '/usr/local/bin/docker build -t pythoncpp/mywebsite .'
            }
        }
        stage ('docker push image') {
            steps {
                sh '/usr/local/bin/docker image push pythoncpp/mywebsite'
            }
        }
        stage ('docker remove service') {
            steps {
                sh '/usr/local/bin/docker service rm myservice'
            }
        }
        stage ('docker create service') {
            steps {
                sh '/usr/local/bin/docker service create --name myservice --replicas 5 -p 9090:80 pythoncpp/mywebsite'
            }
        }
    }
}
