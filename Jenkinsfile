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
            usernamePassword(credentialsId: 'dm_aws_cli'
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

}

// Custom Functions 
// Define your own functions 