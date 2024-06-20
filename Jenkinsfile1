pipeline
{
    agent any
    stages
    {
        stage('1')
        {
            steps
            {
                script
                {
                    git'https://github.com/intelliqittrainings/maven.git'
                }
            }
        }
        stage('2')
        {
            steps
            {
                script
                {
                    sh'mvn package'
                }
            }
        }
        stage('3')
        {
            steps
            {
                script
                {
                    sh'scp /var/lib/jenkins/workspace/dev01P/webapp/target/webapp.war ubuntu@172.31.88.174:/var/lib/tomcat9/webapps/test1.war'
                }
            }
        }
        stage('4')
        {
            steps
            {
                script
                {
                    try
                    {
                        git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                        sh 'java -jar /var/lib/jenkins/workspace/dev01P/testing.jar'
                        
                    }
                    catch(Exception e)
                    {
                        emailext body: '', subject: 'error in git', to: 'dev@dev.com'
                    }
                }
            }
        }
        stage('5')
        {
            steps
            {
                script
                {
                    try
                    {
                        sh'scp /var/lib/jenkins/workspace/dev01P/webapp/target/webapp.war ubuntu@172.31.85.183://var/lib/tomcat9/webapps/prod11.war'
                        
                    }
                    catch(Exception e)
                    {
                        emailext body: 'delivery error', subject: 'error', to: 'prod@gmail.com'
                    }
                }
            }
        }
    }
    
}
