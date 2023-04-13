node {

    stage("Git Clone"){

        git credentialsId: 'GIT_HUB_CREDENTIALS', url: 'https://github.com/sunitabachhav2007/node-todo-cicd.git', branch: 'master' 
    }

     stage("Build") {

       sh 'docker build . -t sunitabachhav2007/node-todo-test:latest'
       sh 'docker image list'

    }

    withCredentials([string(credentialsId: 'DOCKER_HUB_PASSWORD', variable: 'PASSWORD')]) {
        sh 'docker login -u sunitabachhav2007 -p $PASSWORD'
    }

    stage("Push Image to Docker Hub"){
        sh 'docker push sunitabachhav2007/node-todo-test:latest'
    }

    stage("kubernetes deployment"){
        sh 'kubectl apply -f deployment.yml'
    }
}
