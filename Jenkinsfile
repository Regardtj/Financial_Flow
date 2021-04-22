pipeline {
  agent any
  stages {
    stage('Prep_Dev_Environment') {
      steps {
        echo 'Setting Development Environment'
        sh 'id'
        sh 'printenv'
        sh 'ls /usr/local/lib/node_modules/npm/bin'
        sh 'npm -v'
        sh 'ctm -v'
        sh 'echo $PATH'
        sh 'ctm env add Austin_Dev "https://vl-aus-ctm-em01.ctm.bmc.com:8443/automation-api" "rjacobs" "Emd0103@"'
        sh 'ctm env show'
        sh 'ctm env set Austin_Dev'
        echo 'Environment was set to Development'
      }
    }

    stage('Validate') {
      steps {
        echo 'Validate Workflow Syntax'
        sh 'ctm build findev.json'
        echo 'Worklow Build Complete'
      }
    }

    stage('Deploy') {
      steps {
        echo 'Applying Deploy Descriptor Transform and Running Workflow on dev'
        sh 'ctm run findev.json DevDeploy.json -e Austin_Dev'
        echo 'Worklow Run Complete'
      }
    }

    stage('Clean-up') {
      steps {
        echo 'Deleting Development Environment'
        sh 'ctm env delete Austin_Dev'
        echo 'Environment delete Complete'
      }
    }

    stage('Prep_Environment_Prod') {
      steps {
        echo 'Setting Production Environment'
        sh 'ctm env add Austin_Prod "https://vl-aus-ctm-em01.ctm.bmc.com:8443/automation-api" "rjacobs" "Emd0103@"'
        sh 'ctm env show'
        sh 'ctm env set Austin_Prod'
        echo 'Environment was set to Prod'
      }
    }

    stage('Deploy_Workflow_Prod') {
      steps {
        echo 'Applying Deploy Descriptor Transform and Running Workflow'
        sh 'ctm run findev.json ProdDeploy.json -e Austin_Prod'
        echo 'Worklow Run Complete'
      }
    }

    stage('Clean-up Production Environment') {
      steps {
        echo 'Deleting Production Environment'
        sh 'ctm env delete Austin_Prod'
        echo 'Environment delete Complete'
      }
    }

  }
}
