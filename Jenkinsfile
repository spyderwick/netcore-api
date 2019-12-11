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
                sh "rsync -a /var/lib/jenkins/workspace/netCoreAPI_master/Output/ /home/speedy/Documents/mynetcoredll"
            }
        }
        stage('Shell'){
            when{
                branch 'master'
            }
            steps{
                sh "ssh speedy@localhost /home/speedy/Documents/myshell/./svc.sh /home/speedy/Documents/mynetcoredll/servicejson.json"
            }
        }
    }
}

