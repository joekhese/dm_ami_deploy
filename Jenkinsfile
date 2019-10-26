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
}

// Custom Functions 
// Define your own functions 