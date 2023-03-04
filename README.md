pipeline{
    agent any
    stages{
        stage('git Checkout'){
            steps{
                git branch: 'main', url: 'https://github.com/Subashini80/devops.git'
            }
        }
    }pipeline
}