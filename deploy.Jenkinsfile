#!/usr/bin/env groovy

pipeline {
    agent any
    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
        disableConcurrentBuilds()
    }

    stages {
        stage ('Checkout') {
            steps {
                checkout scm
            }
        }
        stage ('Configurer Ansible') {
            steps {
	            sh "rm -rf roles"
	            sh "ansible-galaxy install -f -r requirements.yml"        	    
            }
        }
        stage ('Deploy') {
            steps {
                sh "ansible-playbook -i /cellardoor/env/${env.ENV}/${env.ENV}.hosts -l ${env.HOST} -e x11vnc_action=install -e x11vnc_password=${env.PASSWORD} -e x11vnc_autostart=${env.AUTOSTART} deploy.yml"
            }        
		}
    }

}