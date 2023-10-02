pipeline {
    agent{
        label 'bhavana'
    }
    triggers{
        pollSCM('* * * * *')
    }
    stages{
        stage('vcs') {
           steps{
               git url: 'https://github.com/Praneethysp007/bhavapitstop.git',
                   branch: 'main'

        
            }
        }

        stage('build') {
            steps{
                sh(script: 'dotnet build src/pitstop.sln')


                rtUpload(
                    serverId: 'myinstance',
                    spec: """{
                        "files": [
                            {
                                "pattern": "**/*.dll",
                                "target": "pitstop-generic-local/pitstop-generic-local/"
                            }
                        ]
                    }""" 

                )

            }
        }
        stage('download sonar') {
            steps{
                sh (script: 'dotnet tool install --global dotnet-sonarscanner')

                sh(script: 'env SONAR_TOKEN=22379b81e94c42a9f1e19710a7fa4422402992f0')
            }
        }
        stage('sonar') {
            steps{
                
                withSonarQubeEnv('SONAR_CLOUD') {
                    dotnet sonarscanner begin -Dsonar.organization=myorganisationysp -Dsonar.projectKey=myorganisationysp_pitstop   sh "dotnet build src/pitstop" dotnet sonarscanner end
              }
           }
        }

        stage('results') {
            steps{
                archiveArtifacts artifacts : '**/*.dll'
            }
        }    
    }    
        

}