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

            sh dotnet build src/NopCommerce.sln  


           }
        }
         stage('results') {
            steps{
                archiveArtifacts artifacts: '**/*.dll'
            }
        }       
    }
}    
