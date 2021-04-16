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
        
        stage('SonarCloud') {
            environment {
                SCANNER_HOME = tool 'sonar_scanner'
                ORGANIZATION = "rbkore-github"
                PROJECT_NAME = "rbkore_jenkins-pipeline-as-code"
  }
            steps {
                withSonarQubeEnv('sonar_server') {
                sh '''$SCANNER_HOME/bin/sonar-scanner -Dsonar.organization=$ORGANIZATION \
                -Dsonar.java.binaries=build/classes/java/ \
                -Dsonar.projectKey=$PROJECT_NAME \
            -Dsonar.sources=.'''
                 }
            }
        }
    }
}
