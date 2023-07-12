pipeline {
    agent ( any )
    triggers {
        cron ( "H/5 * * * *" )
    }
    parameters {
        string (name: 'MAVEN_GOAL', defaultValue: 'package', description: 'Maven Goal')
    }
    stages {
        stage ( clone ) {
            steps {
                git url: 'https://github.com/wakaleo/game-of-life.git'
                    branch: "main"
            }
        }
        stage ( build ) {
            steps{ 
                 sh 'export PATH=$PATH:/usr/lib/jvm/java-1.8.0-openjdk/bin' 
                 sh 'mvn ${params.MAVEN_GOAL}'
            }
               
        }
        stage ( sonaranalysis) {
            steps {
                withSonarQubeEnv('SONAR_QUBE') {
                    sh 'mvn sonar:sonar'
                }
            }  
        }
        
    }
}
