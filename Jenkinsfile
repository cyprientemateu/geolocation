pipeline{
   agent any
   tools {
    maven 'M2_HOME'
   }
   stages {
    stage('Code Build') {
        steps {
            sh 'mvn clean package'
        }
    }

    stage('Test') {
        steps {
            sh 'mvn test'
        }
    }

    stage('Upload Artifact') {
        steps {
            nexusArtifactUploader artifacts:
             [[artifactId: '${POM_ARTIFACTID}',
              classifier: '',
               file: 'target/${POM_ARTIFACTID}-${POM_VERSION}.${POM_PACKAGING}',
                type: '${POM_PACKAGING}']],
                 credentialsId: 'nexusID',
                  groupId: '${POM_GROUPID}',
                   nexusUrl: '192.168.33.10:8081',
                    nexusVersion: 'nexus3',
                     protocol: 'http',
                      repository: 'biom1',
                       version: '${POM_VERSION}'
        }
    }
   } 
}   