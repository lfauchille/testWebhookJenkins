node {
    try {
    stage('Checkout') {
        checkout scm
        echo "Build Started"
    }

    stage('Test') {
        echo "Skip"
        //docker.build("${imageName}:${env.BUILD_ID}", "-f Dockerfile.test .")
        //sh "docker run --rm ${imageName}:${env.BUILD_ID}"
    }

    stage('Build') {
        docker.build("pythontest:${env.BUILD_ID}")
        sh 'docker run --rm -p 80:8000 pythontest:${env.BUILD_ID}'
    }

    }catch(e){
        currentBuild.result = 'FAILED'
        throw er
    }finally{
        echo currentBuild.result
    }
}