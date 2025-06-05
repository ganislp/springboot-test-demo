pipeline{
    agent any
    stages{
        stage('Build'){
         agent{

            docker{
                image 'maven:3.8.3-openjdk-17'
                reuseNode true
            }
         }
            steps{
                sh'''
                ls -al
                mvn clean install
                ls -al
                '''
            }
        }
    stage('Test'){
        agent{
            docker{
                image 'maven:3.8.3-openjdk-17'
            }
        }
        steps{
            sh'''
            mvn test
            '''
        }
    }    
        
    }
}