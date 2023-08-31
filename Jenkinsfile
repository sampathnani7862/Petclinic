pipeline {
    agent any 
    
    tools{
        jdk 'jdk17'
        maven 'maven3'
    }
    
     stages{
        
        stage("Git Checkout"){
            steps{
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/sampathnani7862/Petclinic.git'
            }
        }
        
        stage("Compile"){
            steps{
                sh "mvn clean compile"
            }
        }
        
         stage("Test Cases"){
            steps{
                sh "mvn test"
            }
        }
     }
     stage("Build"){
            steps{
                sh " mvn clean install"
            }
        }
        
        stage("Docker Build & Push"){
            steps{
                script{
                   withDockerRegistry(credentialsId: 'dckr_pat_olC78-1QHjpJph5y9AKyg2wwtnY', toolName: 'docker') {
                        
                        sh "docker build -t image1 ."
                        sh "docker tag image1 writetoritika/pet-clinic123:latest "
                        sh "docker push writetoritika/pet-clinic123:latest "
                    }
                }
            }
        }
}
