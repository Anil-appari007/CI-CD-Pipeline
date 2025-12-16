def config = [
            ['dev':['bucket':'devbucket','dist':'1234']],
            ['preprod':['bucket':'prebucket','dist':'5555']],
            ['prod':['bucket':'prodbucket','dist':'9999']],
        ]

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

                    if (env.BRANCH_NAME == 'master') {
                        def prodConfig = config.prod
                        println "Prod bucket = ${prodConfig.bucket}"
                        println "Prod dist   = ${prodConfig.dist}"
                    }
                }
            }
        }
    }
}   