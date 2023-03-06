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
                SET PATH=%PATH%;C:\Program Files\Git\bin;
                sh 'ls'
            }
        }
    }   
}