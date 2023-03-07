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
}

