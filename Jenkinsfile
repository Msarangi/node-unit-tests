pipeline{
    agent any
    environment {
        HTTP_PROXY = 'http://proxy.intra.bt.com:8080'
        HTTPS_PROXY = 'https://proxy.intra.bt.com:8080'
    }
    tools {nodejs "Node-Build"}
    stages {
        stage('Install Dependencies') {
            steps {
                sh'pwd'
                sh'node --version'
                sh'npm --version'
                echo "Installing dependencies"
                //sh'npm install -D sonarqube-scanner'
            }
        }
        stage ('build') {
            steps{
                echo "Building"
                sh 'npm run clean’
                sh 'npm run build'
                }
        }
        stage('Test') {
            steps {
                sh 'npm test'
            }
        }
        stage('SonarQube'){
            environment {
                scannerHome=tool 'sonar_scanner'
            }
            steps{
                withSonarQubeEnv(credentialsId: 'sonar_token', installationName: 'sonar_server') {
                  //sh '${scannerHome}/bin/sonar-scanner -Dproject.settings=./sonar-project.properties'
                  sh """
                  ${sonarscanner}/bin/sonar-scanner
                
                  """
                  //sh "${scannerHome}/bin/sonar-scanner"
                }
             }
        }    
    }
}    
