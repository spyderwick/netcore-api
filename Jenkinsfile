 pipeline{
    agent any
    stages{
        stage('Master Build'){
            when{
                branch 'master'
            }
            steps{
                sh "dotnet restore"
                sh "dotnet clean"
                sh "dotnet build"
                sh "dotnet publish -c release -o ./Output/"
            }
        }

        stage('Test Build'){
            when{
                branch 'dev'
            }
            steps{
                sh "dotnet restore"
                sh "dotnet clean"
                sh "dotnet build"
                sh "dotnet publish -c release -o ./Output/"
                sh "dotnet test --logger 'trx;LogFileName=test1.trx' -r ./Output/Results/" 
                //mstest testResultsFile:"**/*.trx", keepLongStdio: true
            }
        }
        stage('Rsync'){
            when{
                branch 'master'
            }
            steps{
                //sh "rsync -a /var/lib/jenkins/workspace/scriptedPipelineGitHub/Output/ speedy@localhost:/home/speedy/Documents/mydotnetprogramdll/"
            }
        }
        stage('Restart Daemon'){
            steps{
                //sh "ssh speedy@localhost sudo systemctl restart dotnetservice.service"
            }
        }
		
    } 
    post{
        always{
            echo 'This will always runnnnn'
        }
        success{
            echo 'This will run only if successful'
        }
        failure{
            echo 'This will run only if failed'
        }
        unstable{
            echo 'This will run only if the run was marked unstable'
        }
        changed{
            echo 'this will run only if the state of the Pipeline has changed'
            echo 'For Example, if the pipeline was previously failing but is now successful'
        }
    }
}

