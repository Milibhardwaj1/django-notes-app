@Library("Shared") _
pipeline{
    agent{label "vinod"}
    stages{
        stage("Hello"){
            steps{
                script{
                    hello()
                }
            }
        }
        stage("Clone the code"){
            steps{
                echo "This is checking if the repo is already cloned"
                script {
                    if (!fileExists('.git')) {
                        clone("https://github.com/Milibhardwaj1/django-notes-app.git", "main")
                    } else {
                        echo "Repo already cloned, skipping fetch"
                    }
                }
            }
        }
        stage("Build Image"){
            steps{
                script{
                    docker_build("notes-app", "latest", "milibh98")
                }
            }
            
        }
        stage("Deploy"){
            steps{
                echo "This is deploying the code"
                sh "docker compose up -d"
            }
        }
        stage("Push"){
            steps{
                docker_push("notes-app","latest", "milibh98")
            }
        }
    }
}
