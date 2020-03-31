pipeline{
    tools{
        jdk 'myjava'
        maven 'mymaven'
        
    }
    agent any
    stages{
        stage('checkout'){
            steps{
                git 'https://github.com/devops-trainer/DevOpsClassCodes.git'
            }
            
        }
        stage('compile'){
            steps{
              sh 'mvn compile'  
            }
            
        }
        stage('codeReview'){
            steps{
                sh 'mvn pmd:pmd'
            }
            post{
                always{
                    pmd pattern: 'target/pmd.xml'
                    
                }
            }
        }
        stage('unittest'){
            steps{
                sh 'mvn test'
                
            }
            post{
                always{
                    junit 'target/surefire-reports/*.xml'
                    
                }
            }
            
        }
        stage('metriccheck'){
            steps{
                sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
            }
            post{
                always{
                    cobertura coberturaReportFile: 'target/site/cobertura/coverage.xml'
                    
                }
            }
        }
        stage('package'){
            steps{
                sh 'mvn package'
            }
            
        }
    }
}
