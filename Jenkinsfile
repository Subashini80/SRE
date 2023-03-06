pipeline { 
    agent any
    environment {
        PATH = "C:/Program Files/Git/bin:${env.PATH}"
    }
    stages{
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