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
    }
 }   
