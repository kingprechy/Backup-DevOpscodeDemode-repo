        pipeline{
            tools{
                jdk 'Java'
                maven 'maven'
            }
            agent any
            stages{
                stage('Checkout'){
                    agent any
                    steps{
                echo 'cloning...'
                        git 'https://github.com/RayItern/DevOpsCodeDemo-1.git'
                    }
                }
                stage('Compile'){
                    agent {label 'node1'}
                    steps{
                        echo 'compiling...'
                        sh 'mvn compile'
                }
                }
                stage('CodeReview'){
                    agent {label 'node2'}
                    steps{
                    
                echo 'codeReview...'
                        sh 'mvn pmd:pmd'
                    }
                }
                stage('UnitTest'){
                    agent {label 'node2'}
                    steps{
                    echo 'Testing'
                        sh 'mvn test'
                    }
                    post {
                    success {
                        junit 'target/surefire-reports/*.xml'
                    }
                }	
                }
                stage('Package on master') {
            agent {
                label 'master'
            }
            steps {
                echo 'Packaging...'
                sh 'mvn package'
            }
        }
    }
}


