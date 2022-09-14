pipeline{
    agent {label 'slave1'}
    //environment {
      //  PATH = "$PATH:/opt/apache-maven-3.8.2/bin"
    //}
    stages{
       stage('GetCode'){
            steps{
               sh '''
               whoami
               git clone https://github.com/Sharath8000/mydockerapp.git                
               
               '''
            }
         }        
        stage('Docker image build'){
              steps {
                    sh '''
                    
                    echo " *********** Building the image **************"
                    ls -ltra
                    docker build -t firstsapp .
                    
                    echo " ********** Login to Nexus DTR ************* "
                    docker login -u admin -p admin@123 http://34.226.202.185:9001/repository/dockerdtr/
                    
                    echo " ********** Tagging the image ************"
                    docker tag firstsapp 34.226.202.185:9001/repository/dockerdtr/vikas-sharath:myapp.1.0                
                    
                    echo "********** Push to Nexus DTR *************"
                    docker push 34.226.202.185:9001/repository/dockerdtr/vikas-sharath:myapp.1.0
                    
                    echo " ********** Logging out from  Nexus DTR *********** "
                    docker logout http://34.226.202.185:9001/repository/dockerdtr/
                    
                    echo "Image has been pushed to Nexus DTR"
                    
                    ls -ltra
                    pwd
                    
                    '''
              }
         }
    }
   /* post {
        cleanup {
            sh '''
            echo "inside cleanup phase"
            ls -ltra
            echo "going one step back"
            cd ..
            ls -ltra
            rm -rf *
            echo "Files are deleted......."
            
            '''
        }
    }*/
}
