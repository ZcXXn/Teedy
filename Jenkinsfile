pipeline {
    agent any
    stages {
        stage('Build') { 
            steps {
                bat 'mvn clean package' // 使用 Maven 打包项目
            }
        }
        stage('Doc') { 
            steps {
                bat 'mvn javadoc:jar' // 生成 javadoc
            }
        }
        stage('pmd') {
            steps {
                bat 'mvn pmd:pmd' // 运行 PMD 静态代码分析
            }
        }
        stage('Test report') { 
            steps {
                bat 'mvn test' // 运行测试
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
            archiveArtifacts artifacts: '**/target/surefire-reports/*.xml', fingerprint: true // 添加测试报告
            archiveArtifacts artifacts: '**/target/site/apidocs/**', fingerprint: true // 添加 javadoc
        }
    }
}
