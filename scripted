node('built-in') 
{
    stage('continuousDownload')
    {
        git 'https://github.com/intelliqittrainings/maven.git'
    }
    stage('continuousBuild')
    {
        sh 'mvn package'   
    }
    stage('continuousDeployment')
    {
         deploy adapters: [tomcat9(credentialsId: '142f0788-1cbe-4f05-b60d-572f2dd75ab3', path: '', url: 'http://172.31.86.171:8080')], contextPath: 'testapp', war: '**/*.war'
    }
    stage('continuousTesting')
    {
        git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
        sh 'java -jar /home/ubuntu/.jenkins/workspace/scripted/testing.jar'
    }
    stage('continuousDelivery')
    {
        deploy adapters: [tomcat9(credentialsId: '774e5422-db43-49bf-943b-0efdc4fe68bd', path: '', url: 'http://172.31.82.127:8080')], contextPath: 'prodapp', war: '**/*.war'
    }
}
