pipeline {
    agent any

    stages {
        stage('clone git repo') {
            steps {
                echo 'cloning git repository'
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/intelliqittrainings/maven.git']])
            }
        }
        stage('build') {
            steps {
                echo 'building war file using maven'
                sh 'mvn clean install'
            }
        }
        stage('deploy using tomcat container') {
            steps {
                echo 'deploy using tomcat'
                deploy adapters: [tomcat8(credentialsId: 'tomcat', path: '', url: 'http://172.31.27.32:8082')], contextPath: null, war: '**/*.war'
            }
        }
    }
}

