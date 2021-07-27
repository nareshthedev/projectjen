node('master') 
{
    stage('Continous Download')
    {
        git 'https://github.com/intelliqittrainings/maven.git'
    }
    stage('Continous Build')
    {
        sh 'mvn package'
    }
    stage('Continous Deployment')
    {
        deploy adapters: [tomcat9(credentialsId: '00570162-a09e-4a2d-9be8-16dc7ca0503c', path: '', url: 'http://172.31.13.111:8080')], contextPath: 'newapp', war: '**/*.war'
    }
    stage('Continous Testing')
    {
       git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
       sh 'java -jar /var/lib/jenkins/workspace/Scriptedpipeline/testing.jar'
    }
    stage('Continous Delivery')
    {
     deploy adapters: [tomcat9(credentialsId: '00570162-a09e-4a2d-9be8-16dc7ca0503c', path: '', url: 'http://172.31.38.200:8080')], contextPath: 'prodapp', war: '**/*.war'
    }
}
