// pick random github api key from the [0..3] indexed list
// to avoid github api rate limits
Random random = new Random(); def githubCredentialsId = "jenkins-github-api-key-for-terraform-${random.nextInt(3)+1}"
echo "Using ${githubCredentialsId} for github access"
runPipeline('terraflow') {
    platform = 'terraform'
    appName = 'terraform-github-membership'
    baseContainerVersion = '0.11.8'
    terraParallelism = 1
    terraform_secrets = [
      [$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'operational-jenkins-dev-user', accessKeyVariable: 'TF_VAR_backend_aws_access_key', secretKeyVariable: 'TF_VAR_backend_aws_secret_key'],
      [$class: 'UsernamePasswordMultiBinding', credentialsId: "${githubCredentialsId}", usernameVariable: 'TF_VAR_github_username', passwordVariable: 'TF_VAR_github_token']
    ]
}
