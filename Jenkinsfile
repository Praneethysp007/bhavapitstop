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
                rtDotnetResolver (
                    id : 'pitstoppipeline',
                    serverid : 'myinstance',
                    repo : 'mypitstop-nuget-local' 
                )
                rtDotnetRun(
                    args : 'build src/pitstop.sln',
                    resolverid : 'pitstoppipeline' 
                )
                rtPublishBuildInfo(
                    serverid: 'newinstance'
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