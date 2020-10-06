pipeline {
    agent any
    stages { 
        stage ('Prepare') {
            steps {
                checkout([$class: 'GitSCM',
                    branches: [[name: "origin/develop"]],
                    doGenerateSubmoduleConfigurations: false,
                    extensions: [[$class: 'LocalBranch']],
                    submoduleCfg: [],
                    userRemoteConfigs: [[
                        credentialsId: 'manishgithub',
                        url: 'https://github.com/manishraj061/testingpullrequest.git']]])
            }
        }
        stage ('Build') {
            when {
                expression {
                    GIT_BRANCH = 'origin/' + sh(returnStdout: true, script: 'git rev-parse --abbrev-ref HEAD').trim()
                    return GIT_BRANCH == 'origin/develop'
                }
            }
            steps {
                echo "Branch is ${GIT_BRANCH}"
            }
        }		
    }
	post {
      success {
	       echo 'Merging code to Master branch'
                checkout([$class: 'GitSCM',
                    branches: [[name: "origin/master"]],
                    doGenerateSubmoduleConfigurations: false,
                    extensions: [$class: 'PreBuildMerge',options:[mergeTarget: 'master',mergeRemote: 'origin',]],
                    submoduleCfg: [],
                    userRemoteConfigs: [[
                        credentialsId: 'manishgithub',
                        url: 'https://github.com/manishraj061/testingpullrequest.git']]])		   
        }
      success {
	       echo 'develop branch has been merged'
        }	
    }
}
