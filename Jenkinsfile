pipeline{
    
    agent any 
    
    stages {
        
        stage('Git Checkout'){
            
            steps{
                
                script{
                   sh  'mvn clean package sonar:sonar'
                    //git branch: 'main', url: 'https://github.com/tinkusaini13/sonar-demo-app.git'
                   // sh 'mvn sonar:sonar -Dsonar.host.url=http://13.235.134.96:9000  -Dsonar.login=${sonar-api}'
                }
            }
        }
        stage('UNIT testing'){
            
            steps{
                
                script{
                    
                    sh 'mvn test'
                }
            }
        }
        stage('Integration testing'){
            
            steps{
                
                script{
                    
                    sh 'mvn verify -DskipUnitTests'
                }
            }
        }
        stage('Maven build'){
            
            steps{
                
                script{
                    
                    sh 'mvn clean install'
                }
            }
        }
        stage('Static code analysis'){
            
            steps{
                
                script{
                    
                    withSonarQubeEnv(credentialsId: 'sonar-api') {
                        
                        sh 'mvn sonar:sonar -Dsonar.host.url=http://13.235.134.96:9000  -Dsonar.login=admin -Dsonar.password=${sonar-api}'

                    }
                   }
                    
                }
            }
            stage('Quality Gate Status'){
                
                steps{
                    
                    script{
                        
                        waitForQualityGate abortPipeline: false, credentialsId: 'sonar-api'
                    }
                }
            }
        }
        
}
