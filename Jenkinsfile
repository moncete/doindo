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
                        /kaniko/executor -f ./Dockerfile -c `pwd`--insecure --skip-tls-verify --cache=true --destination=10.152.183.142:8081/repository/jenkins/test:""${ent}""
                    '''
                }
            }
        }
    }
}