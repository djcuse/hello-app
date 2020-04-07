node {
    // Get Artifactory server instance, defined in the Artifactory Plugin administration page.
    def server = Artifactory.server "deploy"
    // Create an Artifactory Maven instance.
    def rtMaven = Artifactory.newMavenBuild()
    def buildInfo
  
    
 rtMaven.tool = "maven"

    stage('Clone sources') {
        git url: 'https://github.com/djcuse/hello-app.git'
    }

stage ('Build App') {
sshPublisher(publishers: [sshPublisherDesc(configName: 'Ansible', 
transfers: [sshTransfer(cleanRemote: false, excludes: '', 
execCommand: '''ansible-playbook -i /opt/docker/hosts /opt/docker/docker-create-push-webapp.yml --limit localhost

ansible-playbook -i /opt/docker/hosts /opt/docker/docker-pull-run-webapp.yml --limit 18.219.48.84''', execTimeout: 120000, flatten: false, 
makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', 
remoteDirectory: '//opt/docker', 
remoteDirectorySDF: false, 
removePrefix: 'webapp/target/', 
sourceFiles: 'webapp/target/*.war')], 
usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
  }
}
