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
                        git 'https://github.com/imrans297/Maven-Jenkins.git'
                    }
                    catch(Exception e1)
                    {
                        mail bcc: '', body: 'Jenkins is unable to download Dev code from GITHUB.', cc: '', from: '', replyTo: '', subject: 'Download Fails', to: 'git_team@gmail.com'
                        exit(1)
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
                        sh 'mvn clean install package'
                    }
                    catch(Exception e2)
                    {
                        mail bcc: '', body: 'Jenkins is unable to create an artifact from the code', cc: '', from: '', replyTo: '', subject: 'Build failed', to: 'developers@outlook.com'
                        exit(1)
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
                        deploy adapters: [tomcat9(credentialsId: '5c857de3-a7ad-4013-b04a-ae873aab9ac9', path: '', url: 'http://172.31.27.71:8080')], contextPath: 'testapp', war: '**/*.war'
                    }
                    catch(Exception e3)
                    {
                        mail bcc: '', body: 'Jenkins is unable to deploy into tomcat on the QaServers', cc: '', from: '', replyTo: '', subject: 'Deployment failed', to: 'middleware@outlook.com'
                        exit(1)
                    }
                }
            }
            
        }
        stage('Continous Testing')
        {
            steps
            {
                script
                {
                    try
                    {
                        git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                        sh 'java -jar /var/lib/jenkins/workspace/Declerative-Pipeline/testing.jar'
                    }
                    catch(Exception e4)
                    {
                        mail bcc: '', body: 'Functional testing of the app on QAServers failed', cc: '', from: '', replyTo: '', subject: 'Testing failed', to: 'testing_team@outlook.com'
                        exit(1)
                    }
                }
            }
            
        }
        stage('Continous Deploye')
        {
            steps
            {
                script
                {
                    try
                    {
                        input 'wating for Approval of Delivery Manager!!!'
                        deploy adapters: [tomcat9(credentialsId: '5c857de3-a7ad-4013-b04a-ae873aab9ac9', path: '', url: 'http://172.31.28.123:8080')], contextPath: 'prodapp', war: '**/*.war'
                    }
                    catch(Exception e5)
                    {
                        mail bcc: '', body: 'Unable to deploy into ProdServers', cc: '', from: '', replyTo: '', subject: 'Delivery failed to Prod ENV', to: 'delevery@outlook.com'
                        exit(1)
                    }
                }
            }
            
        }
    
    }    
}    
