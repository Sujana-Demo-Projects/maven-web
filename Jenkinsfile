pipeline{
    agent any
    tools {
        maven 'Maven-3.8.6'
        
    }
    options {
        buildDiscarder logRotator(artifactDaysToKeepStr: '3', artifactNumToKeepStr: '3', daysToKeepStr: '3', numToKeepStr: '3')
        timestamps()
    }
    stages{
        stage("CheckOutCodeFromGitHub"){
            steps{
                git 'https://github.com/Sujana-Demo-Projects/maven-web-application.git'
            }
        }
        stage("BuildingPackage"){
            steps{
                sh "mvn clean package"
            }
        }
        stage("SourceCodeQualityTestingUsingSonarQube"){
            steps{
                    sh 'mvn sonar:sonar'
            }
        }
        stage("StoringPackageInJFrog"){
            steps{
                sh "mvn deploy"
            }
        }
        stage("DeploymentUsingAnsible"){
            steps{
                sh "ansible-playbook ansibledeployment.yaml"
            }
        }
    }
}
