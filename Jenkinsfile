pipeline {
  agent any
 stages {
  stage('Build') {
            steps {
                echo "Building ..."
                bat 'npm install'
                bat 'npm run build'
                echo "Build Successful"
            }
        } 
   stage('Deploy') {
            steps {
                echo 'Deploying....'
                withCredentials([[ $class: 'AmazonWebServicesCredentialsBinding',
                                    credentialsId: "aws-new-creds",
                                    //accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                                    //secretKeyVariable: 'AWS_SECRET_ACCESS_KEY'
                                    ]]) {}
                                    echo "Removing all files on bucket"
                    bat 'aws s3 rm s3://bhabani-1997-bhera --recursive'
                    echo "Attempting to upload site .."
                    echo "Command:  aws s3  sync "
                    bat 'aws s3 sync . s3://bhabani-1997-bhera'
                    echo "S3 Upload complete"
                    bat 'aws s3 ls s3://bhabani-1997-bhera'
                    echo "Invalidating cloudfrond distribution to get fresh cache"
                    //bat 'aws cloudfront create-invalidation --distribution-id=E3BWCA338M4V51 --paths / --profile=myawsprofile'
                    echo "Deployment complete" 
            }
   }
 }
}
