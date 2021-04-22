pipeline {
  agent any
  stages {
    stage('Development_Setup') {
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

    stage('Validate_Dev') {
      steps {
        echo 'Validate Workflow Syntax'
        sh 'ctm build findev.json'
        echo 'Worklow Build Complete'
      }
    }

    stage('Deploy_Dev') {
      steps {
        echo 'Applying Deploy Descriptor Transform and Running Workflow on dev'
        sh 'ctm run findev.json -e Austin_Dev'
        echo 'Worklow Run Complete'
      }
    }

    stage('Clean-up_Dev') {
      steps {
        echo 'Deleting Development Environment'
        sh 'ctm env delete Austin_Dev'
        echo 'Environment delete Complete'
      }
    }

    stage('Production_Setup') {
      steps {
        echo 'Setting Production Environment'
        sh 'ctm env add Austin_Prod "https://vl-aus-ctm-em01.ctm.bmc.com:8443/automation-api" "rjacobs" "Emd0103@"'
        sh 'ctm env show'
        sh 'ctm env set Austin_Prod'
        echo 'Environment was set to Prod'
      }
    }

    stage('Validate_Prod') {
      steps {
        echo 'Validate Workflow Syntax'
        sh 'ctm build findev.json'
        echo 'Worklow Build Complete'
      }
    }

    stage('Deploy_Prod') {
      steps {
        echo 'Applying Deploy Descriptor Transform and Running Workflow'
        sh 'ctm run findev.json ProdDeploy.json -e Austin_Prod'
        echo 'Worklow Run Complete'
      }
    }

    stage('Clean-up_Prod') {
      steps {
        echo 'Deleting Production Environment'
        sh 'ctm env delete Austin_Prod'
        echo 'Environment delete Complete'
      }
    }

  }
}
