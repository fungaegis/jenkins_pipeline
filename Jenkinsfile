#!/usr/bin/env groovy 
pipeline{
    agent none
    parameters {
        choice choices: ['地址1', '地址2', '地址3'], description: '', name: 'git地址'
        // sonarqubescanner = tool 'SonarQubeScanner'
    }
    tools {
        // sonarqubescanner 'SonarQubeScanner'
    }
    post { // post部分应放在Pipeline末端
    always {
        echo 'This will always run'
        }
    success {
        echo 'This will run only if successful'
        }
    failure {
        echo 'This will run only if failed'
        }
    unstable {
        echo 'This will run only if the run was marked as unstable'
        }
    }
    stages{
        stage('单元测试'){
            echo 'unit testing' // 单元测试的结果提供给sonar
        }
        stage('SonarQube静态检查') {
            echo "静态检查完成"
            // steps{
            //     withSonarQubeEnv('sonarqube') { //进入sonarqube环境
            //       sh "${sonarqubeScannerHome}/bin/sonar-scanner -Dsonar.projectKey=jenkins -Dsonar.sources=${WORKSPACE}/code/  -Dsonar.host.url=http://172.16.16.84:9000  -Dsonar.login=${token}"
            //     }
            // }
        }
        stage("质量阀") {        
            echo "质量阀通过"    
            // steps{                  
            //     timeout(time: 1, unit: 'HOURS') {// 超时时间1小时                 
            //         waitForQualityGate abortPipeline: true  // 等待 SonarQube 返回的分析结果。当 abortPipeline=true，表示质量不合格，将 pipeline 状态设置为 UNSTABLE。                
            //     }            
            // }    
        }
        stage("部署环境"){
            stages{
                stage("开发环境"){
                    steps {
                        echo "部署开发环境"
                    }
                }
                stage("测试环境"){
                    steps {
                        echo "部署开发环境"
                    }
                }
                stage("生产环境"){
                    steps {
                        echo "部署开发环境, 请运维人工审批"
                    }
                }
            }
        }
        stage("parallel stage"){
            failFast true
            parallel {
                stage("接口自动化"){
                    agent {
                        label "Docker-Slave"
                    }
                    steps {
                        echo "执行api自动化"
                    }
                }
                stage("组件依赖安全扫描"){
                    agent {
                        label "Docker-Slave"
                    }
                    steps {
                        echo "执行组件依赖安全扫描"
                    }
                }
                stage("UI自动化"){
                    agent {
                        label "Docker-Slave"
                    }
                    steps {
                        echo "执行UI自动化"
                    }
                }
            }
        }
    }
    }
}