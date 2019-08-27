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
                tag = "${ent}"
            }
            steps {
                container (name: 'kaniko', shell: '/busybox/sh') {
                    sh '''
                        #!/busybox/sh
                        echo $tag
                        /kaniko/executor -f ./Dockerfile -c `pwd`--insecure --skip-tls-verify --cache=true --destination=10.152.183.142:18081/test:""${ent}""
                    '''
                }
            }
        }
    }
}