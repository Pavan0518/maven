pipeline
{
    agent any
    stages
    {
        stage('Download')
        {
            steps 
            {
                git 'https://github.com/IntelliqDevops/maven.git'
            }
        }
        stage('Build')
        {
            steps 
            {
                sh 'mvn package'
            }
        }
        stage('Deployment')
        {
            steps 
            {
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'ccfdd5f1-1061-418e-8c62-5acbf61b3cfb', path: '', url: 'http://172.198.74.15:8080')], contextPath: 'mytestapp', war: '**/*.war'
            }
        }
        stage('Testing')
        {
            steps 
            {
                git 'https://github.com/IntelliqDevops/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/ScriptedPipeline1/testing.jar'
            }
        }
        stage('Delivery')
        {
            steps 
            {
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'ccfdd5f1-1061-418e-8c62-5acbf61b3cfb', path: '', url: 'http://172.198.50.58:8080')], contextPath: 'myprodapp', war: '**/*.war'
            }
        }
    }
}