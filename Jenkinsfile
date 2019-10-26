#!/usr/bin/env groovy 

// Import libraries 
import groovy.json.JsonOutput
import groovy.json.JsonSlurper


// Beautify display
def seperator60 = '\u2739' * 60
def seperator20 = '\u2739' * 20


node('misc') {

    stage('Repo Pull') {
        echo "${seperator60}\n${seperator20} Checkout Source Repo \n${seperator60}"
        deleteDir()
        checkout scm 
    }

    stage('Syntax Check') {
        echo "${seperator60}\n${seperator20} Checking packer Syntax \n${seperator60}"
        withCredentials([
            usernamePassword(credentialsId: 'dm_aws_cli',
            passwordVariable: 'AWS_SECRET_ACCESS_KEY',
            usernameVariable: 'AWS_ACCESS_KEY_ID'
        )])
        {
            dir('./'){
                sh"""
                    packer validate packer.json
                    
                """
            }

        }

    }

    // stage("BUILD AMI") {
    //     echo "${seperator60}\n${seperator20} Building Image \n${seperator60}"
    //     withCredentials([
    //         usernamePassword(credentialsId: 'dm_aws_cli',
    //         passwordVariable: 'AWS_SECRET_ACCESS_KEY',
    //         usernameVariable: 'AWS_ACCESS_KEY_ID'
    //     )])
    //     {
    //         dir('./'){
    //             sh """
    //                 packer build packer.json 
    //             """
    //         }
    //     }        
    // }

    stage("Deploy VPC|App|Web Cluster") {
        echo "${seperator60}\n${seperator20} Pause on VPC|App|Web Deployments \n${seperator60}"
        try {
            timeout(time: 30, unit: 'MINUTES') {
                input message: 'Ready to deploy VPC|App|Web Cluster?'
            }
        }
        catch (err) {
            echo "Aborted by user!"
            currentBuild.result = 'ABORTED'
            error('Job Aborted')
        }
    }

    stage('Trigger Next Job') {
        echo "${seperator60}\n${seperator20} Trigeering VPC|WEB|APP Cluster Job \n${seperator60}"
        build(
            job: '2_vpc_web_app_cluster_job',
            wait: 'true'
        )
    } 
}

// Custom Functions docker ps 
// Define your own functions 