pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload')
        {
            steps
            {
                git 'https://github.com/agehma/wed27july.git'
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
                deploy adapters: [tomcat9(credentialsId: '752f12ec-a680-4386-b665-fb804faffad9', path: '', url: 'http://172.31.91.123:8080')], contextPath: 'testapp', war: '**/*.war'
            }
        }
        stage('ContinuousTesting')
        {
            steps
            {
                git 'https://github.com/agehma/testingscript1.git'
                sh 'java -jar /var/lib/jenkins/workspace/DeclaratcivePipeline-Postcon/testing.jar'
            }
        }
    }
    post
    {
        success
        {
            deploy adapters: [tomcat9(credentialsId: '752f12ec-a680-4386-b665-fb804faffad9', path: '', url: 'http://172.31.85.56:8080')], contextPath: 'prodapp', war: '**/*.war'
        }
        failure
        {
            mail bcc: '', body: 'failed to deliver into prodserver tomcat', cc: '', from: '', replyTo: '', subject: 'delivery failed', to: 'anongeric2001@gmail.com'
        }
    }
}



