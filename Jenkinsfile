pipeline {
    agent any

    // 总的步骤
    stages {
        // 第一个步骤
        stage('拉取代码') {
            steps {
                echo '---------------------拉取代码----------------------'

                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: '94051b45-93ce-41b3-ba88-b6d9ec375c35', url: 'https://github.com/690753315/actions-demo1/']])
            }
        }
        // 第二个步骤
        stage('打包') {
            steps {
                echo '---------------------打包----------------------'

                // 使用nodejs 24.7.0 版本
                nodejs('Nodejs 24.7.0'){
                  sh '''
                    node -v
                    npm -v
                    npm i pnpm -g
                    pnpm -v
                    pnpm i
                    pnpm run build
                  '''
                }
            }
        }
        // 第三个步骤
        stage('部署') {
            steps {
                echo '---------------------部署----------------------'

                sshPublisher(publishers: [sshPublisherDesc(configName: '47.115.163.127', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '/docker/nginx/html/my-leyuan2335', remoteDirectorySDF: false, removePrefix: 'dist', sourceFiles: 'dist/**/*')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }

        }
    }
}