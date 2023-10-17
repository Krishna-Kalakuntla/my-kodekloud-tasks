Following code is an example of Jenkins pipeline to clone a git repo, create a docker image from Dockerfile in repo and push it to docker registry.

```

pipeline {
    agent {
        label 'node01'
    }

    stages {
        stage('Build') {
            steps {
                git([url: 'http://git.stratos.xfusioncorp.com/sarah/web.git', branch: 'master', credentialsId: '6fdf8330-8c4a-44aa-a470-f0bfc8b0a4db'])
                script{
                    dockerImage = docker.build "stregi01.stratos.xfusioncorp.com:5000/nginx:latest"
                    docker.withRegistry('http://stregi01.stratos.xfusioncorp.com:5000') {
                        dockerImage.push()
                    }
                } 
                
            }
        }
    }
}

```
