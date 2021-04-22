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
        sh 'ctm run findev.json ProdDeploy.json -e Austin_Dev'
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
        sh 'ctm env add Production "https://cirrocumulus.bmci2t.com:8446/automation-api" "Reggie" "Password"'
        sh 'ctm env show'
        sh 'ctm env set Production'
        echo 'Environment was set to Prod'
      }
    }

    stage('Deploy_Workflow_Prod') {
      steps {
        echo 'Applying Deploy Descriptor Transform and Running Workflow'
        sh 'ctm run findev.json ProdDeploy.json -e Production'
        echo 'Worklow Run Complete'
      }
    }

    stage('Clean-up Production Environment') {
      steps {
        echo 'Deleting Production Environment'
        sh 'ctm env delete Production'
        echo 'Environment delete Complete'
      }
    }

  }
}
