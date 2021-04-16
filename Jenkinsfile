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
        stage("Build")
        {
            steps{
                sh 'mvn clean package'
            }
        }
        
        stage('SonarQube analysis') 
        {
            steps{
                script {
                          def scannerHome = tool 'sonar_scanner';
                          withSonarQubeEnv("sonar_server") {
                          sh "mvn sonar:sonar"
                                       }
                               }
            }
        }
    }
}
