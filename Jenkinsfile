pipeline {
    agent any
    
    stages {
        // Borrado de contenedores en paralelo
        stage('Drop the containers'){   
            parallel{
                stage('Borrar el contenedor Apache')
                {
                        steps{
                        echo 'droping the container...'
                        sh 'docker rm -f app-web-apache'
                        }    
                }
                stage('BORRAR CONTENEDOR NGINX')
                {   
                    steps{
                    echo 'droping the container...'
                    sh 'docker rm -f app-web-nginx'
                    }
                }

            }
            
        }
        //Creating the containers in Parallel
        stage('Create the containers in Parallel') {
            parallel{
                stage('Create the Apache container')
                {           
                    steps {
                    echo 'Creating the Apache Container...'
                    sh 'docker run -dit --name app-web-apache -p 9100:80  -v /home/developer/app-web:/usr/local/apache2/htdocs/ httpd'
                    }
                }
                stage('Create the Nginx container') {
                   steps {
                   echo 'Creating the Apache container...'
                   sh 'docker run -dit --name app-web-nginx -p 9200:80  -v /home/developer/app-web:/usr/share/nginx/html nginx'         
                   }
                }       
            }   
        }
        
    }

    post {              
        success {
        // One or more steps need to be included within each condition's block.
          echo 'The deployment in Nginx and Apache has worked'
          archiveArtifacts allowEmptyArchive: true, artifacts: 'web/*', followSymlinks: false
          cleanWs()         
       }
       failure {
        // One or more steps need to be included within each condition's block.
        echo 'An error has ocurred in the deploy'       
       }
    }
}