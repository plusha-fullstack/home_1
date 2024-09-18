pipeline {
    agent any
    stages {
        stage('Clone') {
            steps {
                git 'git@github.com:plusha-fullstack/home_1.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Deploy to Tomcat') {
            steps {
                sshPublisher(publishers: [sshPublisherDesc(
                    configName: 'Tomcat Server',
                    transfers: [sshTransfer(
                        sourceFiles: '**/target/*.war',
                        removePrefix: 'target',
                        remoteDirectory: '/path/to/tomcat/webapps',
                        execCommand: '/path/to/tomcat/bin/shutdown.sh && /path/to/tomcat/bin/startup.sh'
                    )],
                    usePromotionTimestamp: false,
                    verbose: true
                )])
            }
        }
    }
}
