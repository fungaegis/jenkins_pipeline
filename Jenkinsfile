#!/usr/bin/env groovy 
pipeline {
    agent {
        label 'Docker-Slave-DaoCloud'
    }
    
    stages {
        stage ('Exec Test Command') {
            steps{
                echo 'Build slave container successful'
                sh 'docker -v'  // 查看slave的docker环境是否正常
                sleep 3
                echo 'Destruction slave container successful'
            }
        }
    }
}