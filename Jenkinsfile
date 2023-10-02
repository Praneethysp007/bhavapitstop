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
                rtDotnetRun(
                    args : 'build src/pitstop.sln',
                    resolverid : 'pitstoppipeline' 
                )
                rtDotnetResolver (
                    id : 'pitstoppipeline',
                    serverid : 'myinstance',
                    repo : 'pitstop-nuget' 
                )

                rtPublishBuildInfo(
                    serverid: 'myinstance'
                )
            }
        }

        stage('results') {
            steps{
                archiveArtifacts artifacts : '**/*.dll'
            }
        }    
    }    
        

}