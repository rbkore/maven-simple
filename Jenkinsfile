pipeline{
    agent any
    tools { 
        maven 'M3' 
    
    }
    stages{
        
        stage("Clone")
        {
            steps{
                git 'https://github.com/rbkore/maven-simple'
            }
        }
        
        stage('SonarQube analysis') 
        {
            steps{
                script {
                          def scannerHome = tool 'sonar_scanner';
                          withSonarQubeEnv("sonar_server") {
                          sh "mvn sonar:sonar -Dsonar.host.url=http://localhost:9000"
                                       }
                               }
            }
        }
        
        stage('Test')
        {
            steps{
             sh "mvn test"   
            }
            post {
                always{
                    
                 junit '**/target/surefire-reports/TEST-*.xml'   
                    
                }
                
            }
        }
        
        stage("Build")
        {
            steps{
                sh 'mvn clean package'
            }
        }
        
        
    }
}
