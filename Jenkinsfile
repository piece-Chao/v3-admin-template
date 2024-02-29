pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // 检出代码
                git 'https://github.com/piece-Chao/v3-admin-template.git'
            }
        }
        
        stage('Install dependencies') {
            steps {
                // 安装项目依赖
                sh 'rm -rf node_modules'
                sh 'npmp install'
            }
        }

        stage('Build') {
            steps {
                // 构建项目
                sh 'npm run build:prod'
            }
        }

        stage('Archive') {
            steps {
                // 存档构建产物
                archiveArtifacts artifacts: 'dist/**/*', fingerprint: true
            }
        }

        stage('Deploy') {
            steps {
                // 在这里可以添加部署到服务器的命令
                // 例如通过 SSH 将构建产物部署到服务器
                sh 'ssh root@124.70.30.74'
                sh 'rm -r /var/www/frontend/v3-admin-template'
                sh 'scp -r dist/* root@124.70.30.74:/var/www/frontend/v3-admin-template'
            }
        }
    }
}
