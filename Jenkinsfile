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
               echo "Sonar Qube Analysis...."
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
                branch "prod"
            }
            steps{
               echo "Deploying to production......"
            }
        }
    }
}
