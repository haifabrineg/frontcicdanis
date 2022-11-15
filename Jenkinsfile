pipeline{
 agent any
     
 
    stages {
        stage('Getting project from Git') {
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], browser: [$class: 'GithubWeb', repoUrl: 'https://github.com/haifabrineg/frontcicdanis.git'], extensions: [], userRemoteConfigs: [[credentialsId: '73311888', url: 'https://github.com/haifabrineg/frontcicdanis.git']]])
            }
        }
        
        
        stage('Cleaning the project') {
            steps{
                sh "mvn -B -DskipTests clean  " 
            }
        }
        
        
        stage('Unit Tests') {
            steps{
                sh "mvn test " 
            }
        }
        
        
        
        stage('Artifact Construction') {
            steps{
                sh "mvn -B -DskipTests package " 
            }
        }
        
         
       /* 
     
        stage('Code Quality Check via SonarQube') {
            steps{
                
             sh " mvn sonar:sonar -Dsonar.projectKey=CICD_Academic_Project -Dsonar.host.url=http://localhost:9000 -Dsonar.login=5f74b4c464cd1ad62d859b40eb6c42eda392d71e"
 
            }
        }*/
        

          stage('Publish to Nexus') {
            steps {
                script {
                    
  sh 'mvn  -B -DskipTests deploy -e'
                
                }
            }
        }
          stage('Build Docker Image') {
                      steps {
                          script {
                            sh 'docker build -t haifa123456/spring-app .'
                          }
                      }
                  }
                  stage('Push Docker Image') {
                      steps {
                          script {
                           withCredentials([string(credentialsId: 'haifa123456', variable: 'dockerhubpwd')]) {
                              sh 'docker login -u haifa123456 -p ${dockerhubpwd}'
                           }
                           sh 'docker push haifa123456/spring-app'
                          }
                      }
                  }
        
        
        stage('Run Spring && MySQL Containers') {
                      steps {
                          script {
                            sh 'docker-compose up -d'
                          }
                      }
                  }
            
        
        
} 
    
   
}
       
