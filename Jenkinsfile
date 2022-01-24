pipeline{
    agent any
    triggers {
      pollSCM '* * * * *'
    }
    stages{
        stage("Maven Build"){
            when{
                branch "develop"
            }
            steps{
               sh "mvn package"
            }
        }
        stage("Sonar Qube"){
            when{
                branch "develop"
            }
            steps{
                    withSonarQubeEnv('sonar7') {
                    sh "mvn sonar:sonar"
                    }
            }
        }
        stage("Sonar Qube Status"){
            when{
                branch "develop"
            }
            steps{
                timeout(time: 1, unit: 'HOURS') {
                //    For this to work, we should add webhook in sonar
                //    http://172.31.3.50:8080/sonarqube-webhook/
                    script{
                        def qg = waitForQualityGate()
                        if (qg.status != 'OK') {
                            error "Pipeline aborted due to quality gate failure: ${qg.status}"
                        }
                    }
                }
            }
        }
        stage("Nexus"){
            when{
                branch "develop"
            }
            steps{
               echo "Uploading artifacts to Nexus....."
            }
        }
        stage("Deploy to QA"){
            when{
                branch "qa"
            }
            steps{
               echo "Deploying to QA......."
            }
        }
        stage("Deploy to Production"){
            when{
                branch "master"
            }
            steps{
               echo "Deploying to production......"
            }
        }
    }
}
