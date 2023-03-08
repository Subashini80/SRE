pipeline { 
    agent any
    stages{
        stage('git checkout'){
            steps{
                git branch: 'main', url: 'https://github.com/Subashini80/SRE.git'
            }
        }
        stage('UNIT testing'){
            steps{
                bat "C:\\ProgramFiles\\apache-maven-4.0.0-alpha-4\\bin\\mvn test"
            }
        }
        stage('Intregration Testing'){
            steps{
              bat "C:\\ProgramFiles\\apache-maven-4.0.0-alpha-4\\bin\\mvn verify -DskipUnitTests"  
            }
        }
        stage('maven build'){
            steps{
               bat "C:\\ProgramFiles\\apache-maven-4.0.0-alpha-4\\bin\\mvn clean install"  
            }
        }
        stage('Static code analysis'){
            steps{   
                script{
                    withSonarQubeEnv(credentialsId: 'sonar-api') {
                         bat "C:\\ProgramFiles\\apache-maven-4.0.0-alpha-4\\bin\\mvn clean package"
                    } 
                }
            }
        }
        stage('upload file to Nexus'){
            steps{
                script{      
                   nexusArtifactUploader artifacts: [[artifactId: 'demo', classifier: '', file: 'target/demo-1.0-SNAPSHOT.jar', type: 'jar']], credentialsId: 'Nexus', groupId: 'maven', nexusUrl: 'localhost:8081/', nexusVersion: 'nexus3', protocol: 'http', repository: 'Nexus-Release', version: '1.0-SNAPSHOT'
                }
            }
        }
    }
}      

