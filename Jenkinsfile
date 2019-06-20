def CONTRAIL_VERSION="r5.1"
def BRANCH="R5.1"
image_name="tungstenfabric/developer-sandbox"
image_tag="r5.1"
pipeline {
  environment {
    CONTRAIL_REGISTRY = "saketats/testbuild"
    registryCredential = 'dockerhub'
    dockerImage = ''
  }
  agent any
  stages {
    stage ("Pushing Docker") {
			steps {
				sh label: '',
				script: 'docker exec  contrail-developer-sandbox bash -c \'set -x; cd /root/contrail-dev-env; export CONTRAIL_CONTAINER_TAG="${CONTRAIL_VERSION}"; sed -i "/CONTRAIL_VERSION/d" common.env; export CONTRAIL_REGISTRY="${CONTRAIL_REGISTRY}"; export CONTRAIL_TEST_REGISTRY="$CONTRAIL_REGISTRY"; sed -i '/CONTRAIL_REGISTRY/d' common.env; sed -i '/CONTRAIL_TEST_REGISTRY/d' common.env; export SB_BRANCH="${BRANCH}"; make containers; export SB_BRANCH="${BRANCH}"; make deployers\''
			}
	}
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }
  }
}
