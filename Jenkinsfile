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
    }   
}