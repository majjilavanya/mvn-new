pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload')
        {
            steps
            {
                git 'https://github.com/majjilavanya/mvn-new.git'
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
            deploy adapters: [tomcat9(credentialsId: 'f24490cf-fe42-4bbe-bedf-593dcc5b4ceb', path: '', url: 'http://172.31.40.60:8080')], contextPath: 'test2', war: '**/*.war'
	    }
        }
        stage('ContinuousTesting')
        {
            steps
            {
               git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
               sh 'java -jar /var/lib/jenkins/workspace/DeclarativePipeline1/testing.jar'
            }
        }
       
    }
    
    post
    {
        success
        {
               deploy adapters: [tomcat9(credentialsId: 'bfb67f1d-2f4e-430c-bb8d-30584116bd00', path: '', url: 'http://172.31.50.204:9090')], contextPath: 'prod1', war: '**/*.war'
        }
        failure
        {
            mail bcc: '', body: 'Continuous Integration has failed', cc: '', from: '', replyTo: '', subject: 'CI Failed', to: 'selenium.saikrishna@gmail.com'
        }
       
    }
    
    
    
    
    
    
}
