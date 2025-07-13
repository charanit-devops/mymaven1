pipeline
{
    agent any
    stages
    {
        stage('ContDownload')
        {
            steps
            {
                git 'https://github.com/charanit-devops/maven.git'
            }
        }
        stage('ContBuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('ContDeployment')
        {
            steps
            {
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: '2ad11d84-633a-48e1-8c97-e50dcf9a4ab2', path: '', url: 'http://172.31.87.2:8080')], contextPath: 'newtestapp', war: '**/*.war'
            }
        }
        stage('ContTesting')
        {
            steps
            {
                git 'https://github.com/charanit-devops/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/pipelinescript/testing.jar'
            }
        }
        stage('ContDelivery')
        {
            steps
            {
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: '2ad11d84-633a-48e1-8c97-e50dcf9a4ab2', path: '', url: 'http://172.31.83.127:8080')], contextPath: 'newprodapp', war: '**/*.war'
            }
        }
    }
}
