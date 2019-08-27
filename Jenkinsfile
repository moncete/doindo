def ent = env.BUILD_NUMBER

pipeline {
    agent {
        kubernetes {
            label 'kaniko'
            defaultContainer 'kaniko'
            yamlFile 'kaniko.yaml'
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
                        /kaniko/executor -f ./Dockerfile -c `pwd`--insecure --skip-tls-verify --cache=true --destination=10.28.107.58:32460/repository/jenkins/test:""${ent}""
                    '''
                }
            }
        }
    }
}