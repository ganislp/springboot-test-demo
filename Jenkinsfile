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
            mvn package -DskipTests=true

            '''
        }
    }

    stage('parallel'){
        parallel{
            stage('step1'){
                steps{
                 sh'''
                echo "step1"
                '''
                }

            }
            stage('step2'){
                 steps{
                 sh'''
                echo "step2"
                '''
                }
            }
        }
    }

        
    }
    post{
        always{
            archiveArtifacts artifacts: "target/*.jar"
            junit 'target/surefire-reports/*.xml'

        }
    }
}