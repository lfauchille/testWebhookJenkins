node('slaves')  {
    try {
    stage('Checkout') {
        checkout scm
        echo "Build Started"
    }

    stage('Build') {
        docker.build("pythontest:${env.BUILD_ID}")
    }
    

    stage('Test') {
        docker.image("pythontest:${env.BUILD_ID}").inside(){
            sh 'python test.py'
        }
        //sh "docker run --rm ${imageName}:${env.BUILD_ID}"
    }

    stage('Run') {
        docker.image("pythontest:${env.BUILD_ID}").inside('-p 8000:8000'){
            sh 'python main.py &'
        }
        // sh 'docker run --rm -p 8000:8000 pythontest:${env.BUILD_ID} python test.py'
    }

    }catch(e){
        currentBuild.result = 'FAILED'
        throw e
    }finally{
        echo currentBuild.result
    }
}