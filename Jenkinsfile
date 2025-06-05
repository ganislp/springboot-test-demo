pipeline{
    agent any
    stages{
        // This is a build 
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
    stage('Unit Test'){
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

    stage('Package'){
        agent{
            docker{
                image 'maven:3.8.3-openjdk-17'
            }
        }
        steps{
            sh'''
            mvn package

            '''
        }
    }
        
    }
    post{
        always{
            archiveartifacts artifacts  : "target/*.jar"
            junit 'target/surefire-reports/*.xml'

        }
    }
}