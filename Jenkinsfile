def dockerContainer
pipeline {
    agent none
    stages {
        // stage('build') {
        //     agent {
        //         docker { image 'gradle' }
        //     }
        //     steps {
        //         sh 'chmod +x gradlew && ./gradlew build'
        //     }
        // }
        // stage('sonarqube') {
        //     agent {
        //         docker { image 'gradle' }
        //     }
        //     steps {
        //         withSonarQubeEnv("SonarCloud") {
        //             sh 'chmod +x gradlew && ./gradlew sonarqube'
        //         }
        //     }
        // }
        // stage('docker build') {
        //     agent {
        //         docker { image 'docker' }
        //     }
        //     steps {
        //         script {
        //             dockerContainer = docker.build('aarondownward/sample-spring-boot')
        //         }
        //     }
        // }
        // stage('docker push') {
        //     agent {
        //         docker { image 'docker' }
        //     }
        //     steps {
        //         sh 'echo docker push'
        //         script {
        //             docker.withRegistry("https://registry.hub.docker.com", "dockerhub-creds") {
        //                 dockerContainer.push()
        //             }
        //         }
        //     }
        // }
        stage('app deploy') {
            agent {
                docker { image 'docker' }
            }
            steps {
                sh 'curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl \
    && chmod +x ./kubectl \
    && mv ./kubectl /usr/local/bin/kubectl'
                sh 'kubectl rollout restart deployment sample-spring-boot -n application'
                // script {
                //     kubernetesDeploy(configs: "kubernetes.yml")
                // }
            }
        }
    }
}