node('built-in') {
 
    stage('Continuous Download')
    {
        // Its a repo for continuous downlad
        git branch: 'main', url: 'https://github.com/sysgeeks4u/Maven-Tomcat.git'
    }

    stage('Continuous Build')
    {
        // ecevute maven command for building application
        sh 'mvn package'
    }

    stage('Continuous Delivery')
    {
        // delivering application on a staging Server
        deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'admin-test', path: '', url: 'http://10.10.10.253:8080/')], contextPath: 'testapp', war: '**/*.war'
    }
    
    stage('Continuous Testing')
    {
        // download Testing software from repo
        git branch: 'main', url: 'https://github.com/sysgeeks4u/Functional-Testing.git'
        
        // ececute testing.jar file
        sh 'java -jar /var/lib/jenkins/workspace/Scripted-Pipeline/testing.jar'
    }

    stage('Continuous Deploy')
    {
        // Deploying Application on live servers/prod servers/client servers
        deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'prod-admin', path: '', url: 'http://10.10.10.247:8080/')], contextPath: 'prodapp', war: '**/*.war'
    }
}

