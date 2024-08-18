pipeline { //pipeline as code - Jenkinsfile
    agent{
        label "rhel"
    }

    stages { //collection of your jobs
        stage('Download the source code') { //stage ~=job
            steps {
               git branch: 'main', url: 'https://github.com/sudhanshuvlog/SnakeGame.git'
               echo "code downloaded succesfully"
            }
        }
        stage('Test'){
            steps{
                sh "yum install python3-pip-21.3.1-2.amzn2023.0.5.noarch -y"
                sh "pip install -r requirements.txt"
                sh "pytest"
                echo "Code have been tested succesfully!"
            }
        }
        stage("Build Docker Image"){
            steps{
                sh "docker build -t gfgwebimg ."
            }
        }
        stage("Deployment"){
            steps{
                sh "docker rm -f webos"
                sh "docker run -dit --name webos -p 5000:5000 gfgwebimg"
            }
        }
    }
}
