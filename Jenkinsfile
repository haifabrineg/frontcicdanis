pipeline{
    agent any


    tools {
        maven 'M2_HOME'
    }


	stages {



/*

        stage('Cleaning the project') {
            steps{
                sh "npm install"
            }
        }





        stage('Artifact Construction') {
            steps{
                sh "ng build  "
            }
        }
*/


stage('Build Docker Image') {
                      steps {
                          script {
                            sh 'docker build -t haifa123456/angular-app:latest .'
                          }
                      }
                  }


/*

                  stage('login dockerhub') {
                                        steps {
                                      sh 'echo dckr_pat_-SnwrdC_ELsL6it2JT6cgIcAlrs | docker login -u azizbenhaha --password-stdin'
                                            }
		  }





	                      stage('Push Docker Image') {
                                        steps {
                                   sh 'docker push azizbenhaha/angular-app:latest'
                                            }
		  }
*/


        stage('Run Angular Container') {
                      steps {
                          script {
                            sh 'docker compose up -d'
                          }
                      }
                  }

}


}
