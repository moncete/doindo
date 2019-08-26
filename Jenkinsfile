pipeline {
    agent {
        kubernetes {
            yamlFile './kaniko.ymal'
        }
    }

    stages {
        stage ('Build and Push Image') {
            environment {
                PATH = "/busybox:/kaniko:$PATH"
            }
            steps {
                container (name: 'kaniko', shell: '/busybox/sh') {
                    sh '''
                        #!/busybox/sh
                        /kaniko/executor -f ./Dockerfile -c `pwd`--insecure --skip-tls-verify --cache=true --destination=10.152.183.58:5000/test
                    '''
                }
            }
        }
    }
}