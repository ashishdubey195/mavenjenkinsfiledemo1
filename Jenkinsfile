pipeline {
    tools{
        maven 'mymaven'
    }
    agent any 
    stages{
        stage ('CloneRepo')
        {
            steps{
             echo 'This is stage 1'
              git 'https://github.com/ashishdubey195/DevOpsCodeDemo.git'
            }
        }
        stage('compile')
        {
            steps{
                sh 'mvn compile'
            }
        }
        stage('code review')
        {
            steps{
                sh 'mvn pmd:pmd'
            }
            post {
                success {
                  recordIssues sourceCodeRetention: 'LAST_BUILD', tools: [pmdParser(pattern: '**/pmd.xml')] 
                }
            }
        }
            stage('Test')
            {
                steps{
                    sh 'mvn test'
                }
                post{
                    success{
                      junit stdioRetention: '', testResults: 'target/surefire-reports/*.xml'  
                    }
                }
            }    
            stage('Package')
            {
                steps{
                    sh 'mvn package'
                }
            }
            
        }
    }

            

