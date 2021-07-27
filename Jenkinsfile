pipeline
{
    agent any
    stages
    {
        stage('Continous Download')
        {
            steps
                {
                    git 'https://github.com/nareshthedev/projectjen.git'
                }
        }
        stage('Continous Build')
        {
            steps
                {
                    sh 'mvn package'
                }
        }
        stage('Continous Deployment')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '00570162-a09e-4a2d-9be8-16dc7ca0503c', path: '', url: 'http://172.31.13.111:8080')], contextPath: 'newapp1', war: '**/*.war'
            }
        }
        stage('Continous Testing')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/Scriptedpipeline/testing.jar'
            }
        }
    }
    post
    {
        success
            {
                input message: 'Need approval from DM', submitter: 'ravi'
                deploy adapters: [tomcat9(credentialsId: '00570162-a09e-4a2d-9be8-16dc7ca0503c', path: '', url: 'http://172.31.38.200:8080')], contextPath: 'prodapp1', war: '**/*.war'
            }
        
        failure
            {
                mail bcc: '', body: 'Continuous Integration failed', cc: '', from: '', replyTo: '', subject: 'Continuous Integration failed', to: 'kumarkarri@yahoo.co.in'
            }
    
    }
}
