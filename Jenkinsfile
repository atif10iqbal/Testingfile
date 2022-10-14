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
        stage('ContinuousDeployment')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: 'ad57bcb9-8931-40f0-9a97-c6d228307ada', path: '', url: 'http://172.31.42.137:8080')], contextPath: 'test', war: '**/*.war'
            }
        }
        stage('ContinuousTesting')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh 'java -jar /home/ubuntu/.jenkins/workspace/DeclrativePipeline-1/testing.jar'
                
            }
        }
        stage('ContinuousDelivery')
        {
            steps
            {
                input message: 'Need Permission From Iqbal Bhai', submitter: 'iqbal'
                deploy adapters: [tomcat9(credentialsId: 'ad57bcb9-8931-40f0-9a97-c6d228307ada', path: '', url: 'http://172.31.42.137:8080')], contextPath: 'app', war: '**/*.war'
            }
        }
    }
}
