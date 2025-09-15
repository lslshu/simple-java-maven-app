pipeline {
    agent {
        docker {
            image 'maven:3-alpine' 
            args '-v /root/.m2:/root/.m2' 
            reuseNode true // 可选：在同一个工作空间内重用节点
        }
    }
    stages {
        stage('Build') { 
            steps {
                // 使用 -B 批处理模式，-q 安静模式（减少日志输出）
                sh 'mvn -B -q clean package' 
            }
        }
        stage('Test') {
            steps {
                // 单独运行测试，便于查看测试结果
                sh 'mvn -B test' 
            }
        }
    }
    post {
        always {
            // 构建后操作：总是归档制品
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
        }
        success {
            echo '构建成功！'
        }
        failure {
            echo '构建失败！'
        }
    }
}
