pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload')
        {
            steps
            {
                git 'https://github.com/sourav88/maven4.git'
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
		deploy adapters: [tomcat9(credentialsId: '9639cbde-e2f2-49f2-95e8-bea934be18d3', path: '', url: 'http://172.31.2.230:8080')], contextPath: 'testapp6', war: '**/*.war'
            }
        }
        stage('ContinuousTesting')
        {
            steps
            {
               git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
               sh 'java -jar /home/ubuntu/.jenkins/workspace/DeclarativePipeline1/testing.jar'
            }
        }
       
    }
    
    post
    {
        success
        {
            input message: 'Need approval from the DM!', submitter: 'srinivas'
		deploy adapters: [tomcat9(credentialsId: '8dccc17f-b77d-4e14-a644-d229ae01cebc', path: '', url: 'http://172.31.12.29:8080')], contextPath: 'prodapp88', war: '**/*.war'
        }
        failure
        {
            mail bcc: '', body: 'Continuous Integration has failed', cc: '', from: '', replyTo: '', subject: 'CI Failed', to: 'selenium.saikrishna@gmail.com'
        }
       
    }
    
    
    
    
    
    
}
