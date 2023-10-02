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
                rtNugetCli(
                    command : 'build'
                    args : 'src/pitstop.sln',
                    resolverid : 'pitstoppipeline' 
                )
                rtNugetResolver (
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