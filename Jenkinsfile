pipeline{
    agent any

    tools{
        maven 'jenkins-maven'
    }
    stages{
        stage("test"){
            steps{
                sh 'mvn test'
            }
           
            }
        stage("build"){
            steps{
                sh 'mvn package'
            }
        }
        stage("test on testing server"){
            steps{
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'tomcat-access', path: '', url: 'http://192.168.247.128:8082')], contextPath: '/hello-world-0.0.1-SNAPSHOT/', war: '**/*.war'
            }
        }
        stage("deploy to production server"){
            input{
                message "should we move ahead"
                ok "move ahead"
            }
            steps{
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'tomcat-access', path: '', url: 'http://192.168.247.143:8082')], contextPath: '/hello-world-0.0.1-SNAPSHOT/', war: '**/*.war'
            }
        }
    }
    
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}
