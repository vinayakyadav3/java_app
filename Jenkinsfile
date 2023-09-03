@Library('jenkins_shared_lib') _

pipeline{

    agent any

    parameters{

        choice(name: 'action', choices: 'create\ndelete', description: 'Choose create/Destroy')

    }
    
    stages{
         
        stage('Git Checkout'){
        when { expression {  params.action == 'create' } }
            steps{
                script{
                    
                    gitCheckout(
                    branch: "main",
                    url: "https://github.com/yvinvijay/mrdevops_java_app.git"
            )
                }
            }
        }

        stage('Unit Test maven'){
        when { expression {  params.action == 'create' } } 
            steps{
               script{
                   
                   mvnTest()
               }
            }
        }
        
        stage('Integration Test maven'){
        when { expression {  params.action == 'create' } } 
            steps{
               script{
                   
                   mvnIntegrationTest()
               }
            }
        }

        stage('Static code analysis: Sonarqube'){
         
            steps{
               script{
                   
                   def SonarQubecredentialsId = 'sonarqube-api'
                   statiCodeAnalysis(SonarQubecredentialsId)
               }
            }
        }

    }
}

