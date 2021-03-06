pipeline {
  options {
    buildDiscarder(
      logRotator(
        numToKeepStr: '5',
        artifactNumToKeepStr: '5'
      )
    )
  }
  agent any
  triggers {
    pollSCM('H/5 * * * *')
  }
  stages{
      parallel {
        stage ('checkout: sw-aem-infrastructure') {
          steps {
            dir('sw-aem-infrastructure') {
              git branch: 'master',
                credentialsId: 'ebus-github',
                url: 'https://github.sherwin.com/SherwinWilliams/sw-aem-infrastructure/'
            }
          }
        }
        stage ('checkout: sw-aem-foundation-core') {
          steps {
            dir('sw-aem-foundation-core') {
              git branch: params.SW_AEM_FOUNDATION_CORE_BRANCH,
                credentialsId: 'ebus-github',
                url: 'https://github.sherwin.com/SherwinWilliams/sw-aem-foundation-core/'
            }
          }
        }
        stage ('checkout: sw-aem-connector-data') {
          steps {
            dir('sw-aem-connector-data') {
              git branch: params.SW_AEM_CONNECTOR_DATA_BRANCH,
                credentialsId: 'ebus-github',
                url: 'https://github.sherwin.com/SherwinWilliams/sw-aem-connector-data/'
            }
          }
        }
        stage ('checkout: sw-aem-commons') {
          steps {
            dir('sw-aem-commons') {
              git branch: params.SW_AEM_COMMONS_BRANCH,
                credentialsId: 'ebus-github',
                url: 'https://github.sherwin.com/SherwinWilliams/sw-aem-commons/'
            }
          }
        }
        stage ('checkout: sw-aem-foundation-ui') {
          steps {
            dir('sw-aem-foundation-ui') {
              git branch: params.SW_AEM_FOUNDATION_UI_BRANCH,
                credentialsId: 'ebus-github',
                url: 'https://github.sherwin.com/SherwinWilliams/sw-aem-foundation-ui/'
            }
          }
        }
        stage ('checkout: aem-local') {
          steps {
            dir('sw-aem-repo-test') {
              git branch: 'master',
                credentialsId: 'ebus-github',
                url: 'https://github.com/RamaVollala/AEM_RepoTest.git'
            }
          }
        }
      }
    stage('Build_ConnectorData'){
      when {
        changeRequest target:'https://github.com/RamaVollala/AEM_RepoTest/tree/master'
      }
        steps {
          sh """
            docker build -t aem_connector_build -f ./Build_ConnectorData .
            docker run -d --name aem_connector_build_${JOB_BASE_NAME}_${BUILD_NUMBER} --rm aem_build:latest /bin/sleep 5000
            docker cp aem_connector_build_${JOB_BASE_NAME}_${BUILD_NUMBER}:/sw-aem-connector-data/ui.apps/target/com.sherwin.aem.connector.data.ui.apps-${AEM_CONNECTOR_CODE_VERSION}.zip ./
            docker kill aem_build_${JOB_BASE_NAME}_${BUILD_NUMBER}
          """
        }
    }
  }
}
