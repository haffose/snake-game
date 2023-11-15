node('linode-app-server')
{
    def app
    stage('Clone Git')
    {
    /* Let's make sure we have the respository cloned to our workspace */
    checkout scm
    }
    stage('Build-and-Tag')
    {
        /* This builds the actual image;
        * This is synonymous to docker build on the command line */
        app =docker.build("haffose/snake-game-repo")    
    }
    stage('Post-to-dockerhub')
    {
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub-credentials')
        {
        app.push("latest")
        }
    }
    
    stage('Pull-image-server')
    {
        sh "docker-compose down"
        sh "docker-compose up -d"
    }
}


