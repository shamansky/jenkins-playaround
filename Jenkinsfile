pipeline {
    agent any
    
    stages{
        stage('Verify Branch') {
            steps {
                echo "$GIT_BRANCH"
            }
        }
        stage ('Build') {
          git url: 'https://github.com/cyrille-leclerc/multi-module-maven-project'
             withMaven {
                sh "mvn clean verify"
             } // withMaven will discover the generated Maven artifacts, JUnit Surefire & FailSafe reports and FindBugs reports
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