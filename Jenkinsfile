pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'dotnet build --configuration Release --no-restore eShopOnWeb.sln'
      }
    }

    stage('Tests') {
      parallel {
        stage('Tests') {
          steps {
            sh 'dotnet test tests/UnitTests   --configuration Release   --no-build   --no-restore'
          }
        }

        stage('Integration') {
          steps {
            sh 'dotnet test tests/IntegrationTests.csproj   --configuration Release   --no-build   --no-restore'
          }
        }

        stage('Functional') {
          steps {
            sh 'dotnet test tests/FunctionalTests   --configuration Release   --no-build   --no-restore'
          }
        }

      }
    }

    stage('Deployment') {
      steps {
        sh 'dotnet publish eShopOnWeb.sln -o /var/aspnet'
      }
    }

  }
}