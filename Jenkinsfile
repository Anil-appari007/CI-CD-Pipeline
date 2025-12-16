def config = [
            ['dev':['bucket':'devbucket','dist':'1234']],
            ['preprod':['bucket':'prebucket','dist':'5555']],
            ['master':['bucket':'prodbucket','dist':'9999']],
        ]
def BUCKET = null
def DIST = null
def id = null

pipeline{
    agent any
    triggers {
        pollSCM('* * * * *')
    }
    stages{
        stage("Validate"){
            steps{
                script{
                    println "config - ${config}"
                    // git 'https://github.com/Anil-appari007/CI-CD-Pipeline'
                    checkout scm
                    println "BRANCH_NAME - ${env.BRANCH_NAME}"

                    switch(env.BRANCH_NAME){
                        case 'main':
                            id = 'master'
                            break
                        case 'pre-prod':
                            id = 'preprod'
                            break
                        case 'dev':
                            id = 'dev'
                            break
                        default:
                            error "invalid branch"
                    }
                    println "id - ${id}"
                    def envConfig = config.find { it.containsKey(id) }[id]
                    println "config of branch - ${envConfig}"
                    println "bucket - ${envConfig.bucket}"
                    println "dist - ${envConfig.dist}"

                }
                withCredentials([string(credentialsId: 'ANILS_GIT', variable: 'ANILS_GIT_URL')]) {
                        sh "echo VITE_API_URL=${ANILS_GIT_URL} > .env"
                        sh "cat .env"
                    }
            }
        }
    }
}   