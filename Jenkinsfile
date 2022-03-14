def con_name

pipeline {
    agent {
        label "gpus"
    }
    parameters {
        string(name: "MS_CORE_IMAGE_NAME", defaultValue: "python", description: "")
        string(name: "MS_CORE_IMAGE_TAG", defaultValue: "latest", description: "")
    }
    stages {
        stage('Prepare environment') {
            steps {
                script {
                    con_name = "${env.BUILD_TAG}".replace("/", "_")
                    con_name = "${con_name}".replace("%2F", "_")
                }
            }
        }
        stage('Check environment') {
            steps {
                withDockerContainer(image:"${params.MS_CORE_IMAGE_NAME}:${params.MS_CORE_IMAGE_TAG}", 
                args: "--name check_pipeline_${con_name} --gpus '\"device=${env.GPUs}\"' --ipc=host --entrypoint=\'\'") {
                      sh "pwd"
                      sh "ls -al"
                      sh "id"
                }            
            }
        }
    }
}

