#!/usr/bin/env groovy

pipeline {
	agent any
	stages {
		stage('build-test') {
			steps {
				sh 'dotnet restore'
				sh 'dotnet build'
				sh 'dotnet test --no-build --no-restore'
			}
		}

		stage('build-push-image') {
			steps {
				sh 'dotnet publish ./icc-manager/icc-manager.csproj -c Release -r ubuntu.16.10-x64 -o ./bin/publish'
				sh 'dotnet publish ./icc-manager/icc-manager.csproj -c Release -r win7-x86 -o ./bin/win7/publish'
				sh 'docker build -t home.freemanke.com:25000/freemanke/icc-manager:${BUILD_NUMBER} ./src/icc-manager/'
				sh 'docker push home.freemanke.com:25000/freemanke/icc-manager:${BUILD_NUMBER}'
			}
		}

		stage('deploy-dev') {
			steps {
				sh 'docker stop icc-manager || true && docker rm -f icc-manager || true'
				sh 'docker run -d --name icc-manager -p 33000:33000 home.freemanke.com:25000/freemanke/icc-manager:${BUILD_NUMBER}'
			}
		}
	}
}
