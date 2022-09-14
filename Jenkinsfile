pipeline{
    agent {label 'slave1'}
    //environment {
      //  PATH = "$PATH:/opt/apache-maven-3.8.2/bin"
    //}
    stages{
       stage('GetCode'){
            steps{
                git 'https://github.com/Sharath8000/hello-world.git'
            }
         }        
        stage('Docker image build'){
              steps {
                    sh '''
                    
                    echo " *********** Building the image ***********"
                    docker build -t firstsapp -f ./Dockerfile
                    
                    echo " ********** Login to Nexus DTR *********** "
                    docker login http://34.226.202.185:9001/repository/Docker-Hosted-Repo/
                    
                    echo " ********** Tagging the image ************"
                    docker tag firstapp http://34.226.202.185:9001/repository/Docker-Hosted-Repo/sharath-vikas-dtr/myfirstapp                   
                    
                    echo "********** Push to Nexus DTR *************"
                    docker push http://34.226.202.185:9001/repository/Docker-Hosted-Repo/sharath-vikas-dtr/myfirstapp
                    
                    echo " ********** Logging out from  Nexus DTR *********** "
                    docker logout http://34.226.202.185:9001/repository/Docker-Hosted-Repo/
                    
                    echo "Image has been pushed to Nexus DTR"
                    
                    
                    
                    '''
              }
         }
    }
}
