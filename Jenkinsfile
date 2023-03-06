pipeline { 
    agent any
    stages{
        environment {
            PATH = "/hot/new/bin:${env.PATH}"
        }
        stage('git checkout'){
            steps{
                git branch: 'main', url: 'https://github.com/Subashini80/SRE.git'
            }
        }
        stage('UNIT testing'){
            steps{
                sh 'ls'
            }
        }
    }   
}