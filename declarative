pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/maven.git'
            }
        }
        stage('ContinuousBuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('continuousDeploy')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '774e5422-db43-49bf-943b-0efdc4fe68bd', path: '', url: 'http://172.31.86.171:8080')], contextPath: 'testing', war: '**/*.war'
            }
        }
        stage('ContinuousTesting')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh 'java -jar /home/ubuntu/.jenkins/workspace/declarative/testing.jar'
            }
        }
        stage('ContinuousDelivery')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '774e5422-db43-49bf-943b-0efdc4fe68bd', path: '', url: 'http://172.31.82.127:8080')], contextPath: 'production', war: '**/*.war'
            }
        }
    }
}
