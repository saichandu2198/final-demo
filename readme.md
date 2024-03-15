pipeline {
    agent any

    stages{
        stage('deploy to S3'){
            steps{
               sh 'aws s3 cp public s3://mystaticbucketjenkins --recursive'
               sh 'aws s3api put-bucket-policy --bucket mystaticbucketjenkins --policy file://policy.json'
               sh 'aws s3 website s3://mystaticbucketjenkins/ --index-document index.html --error-document error.html'
             
            }
        }
    }
    
}
