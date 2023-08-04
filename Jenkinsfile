pipeline {


    agent { label 'bhavana' } 

    triggers {
        pollSCM('* * * * *')

    
    }
    tools {
        jdk 'JDK_17'
         
    }

    stages { 
        stage('vcs') {
            steps {
                git url: 'https://github.com/Bhavana-2022/nopcommerce.git',
                    branch: 'develop'
            }
                
        }
        stage('build and package') {
           steps {
                rtDotnetResolver (
                    id : "bhavana",
                    serverId : "bhavanainstance",
                    repo : "commerce-nuget-local"
                ) 
                rtDotnetRun (
                    args : "build src/NopCommerce.sln",
                    resolverId : "bhavana"
                )
                 rtPublishBuildInfo (
                    serverId: "bhavanainstance"
                 )
                 


           }
        }
         stage('results') {
            steps{
                archiveArtifacts artifacts: '**/*.dll'
            }
        }
        stage('sonar-cube') {
            steps{
                withSonarQubeEnv('SONAR_CLOUD') {
                  
                   sh 'mono /home/ubuntu/.dotnet/tools/SonarScanner.MSBuild.exe begin  /o:bhavanamangrathi123  /k:bhavanamangrathi123_qt  /d:sonar.host.url=https://sonarcloud.io dotnet build src/NopCommerce mono /home/ubuntu/.dotnet/tools/SonarScanner.MSBuild.exe end' 

                }
            }
        }       
    }
}    
