pipeline
{
    agent any
    stages
    {
        stage('Continous Download')
        {
            steps
            {    
                script
                {
                    try
                    {
                        git 'https://github.com/nareshthedev/projectjen.git'
                    }
                    catch(Exception e1)
                    {
                        mail bcc: '', body: 'jenkins unable to download code', cc: '', from: '', replyTo: '', subject: 'Continuous Download failed failed', to: 'devadmin@gmail.com'
                    }
                }
            }
        }
        stage('Continous Build')
        {
            steps
            {
                script
                {
                    try
                    {
                        sh 'mvn package'
                    }
                    catch(Exception e2)
                    {
                        mail bcc: '', body: 'code build failed', cc: '', from: '', replyTo: '', subject: 'Continuous build failed', to: 'buildadmin@gmail.com'
                    }
                }
            }
        }
        stage('Continous Deployment')
        {
            steps
            {
                 script
                {
                    try
                    {
                         deploy adapters: [tomcat9(credentialsId: '00570162-a09e-4a2d-9be8-16dc7ca0503c', path: '', url: 'http://172.31.13.111:8080')], contextPath: 'newapp1', war: '**/*.war'
                    }
                    catch(Exception e3)
                    {
                        mail bcc: '', body: 'code  tests failed', cc: '', from: '', replyTo: '', subject: 'Continuous testing failed', to: 'testadmin@gmail.com'
                    }
                }
            }   
        }
        stage('Continous Testing')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/Declarativepipeline2/testing.jar'
            }
        }
        stage('Continous Delivery')
        {
            steps
            {
                input message: 'Need approval from DM', submitter: 'ravi'
                deploy adapters: [tomcat9(credentialsId: '00570162-a09e-4a2d-9be8-16dc7ca0503c', path: '', url: 'http://172.31.38.200:8080')], contextPath: 'prodapp1', war: '**/*.war'
            }
        }
    }
}
