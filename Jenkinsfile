pipeline {
    agent any
    tools {
        maven 'Maven_3.5.2' 
    }
    stages{
        stage('Verify Branch') {
            steps {
                echo "$GIT_BRANCH"
            }
        }
        stage('Docker Build') {
           steps {
              pwsh(script: 'docker images -a')
              pwsh(script: """
              cd azure-vote/
              docker images -a
              docker build -t jenkins-pipeline .
              docker images -a
              cd ..
              """)
           }
        }
    }
}