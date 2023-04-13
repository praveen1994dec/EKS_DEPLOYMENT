node {

    stage("Git Clone"){

        git credentialsId: 'Git_Hub', url: 'https://github.com/praveen1994dec/EKS_DEPLOYMENT.git', branch: 'main' 
    }

     stage("Build") {

       sh 'docker build . -t praveensingam1994/node-test:latest'
       sh 'docker image list'

    }

    withCredentials([string(credentialsId: 'DOCKER_HUB_PASSWORD', variable: 'PASSWORD')]) {
        sh 'docker login -u praveensingam1994 -p $PASSWORD'
    }

    stage("Push Image to Docker Hub"){
        sh 'docker push praveensingam1994/node-test:latest'
    }

    stage("kubernetes deployment"){
        sh 'kubectl apply -f deployment.yml'
    }
}
