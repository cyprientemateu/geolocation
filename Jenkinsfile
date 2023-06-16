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
            script{
                def mavenPom = readMavenPom file: 'pom.xml'

            nexusArtifactUploader artifacts:
             [[artifactId: "${mavenPom.artifactId}",
              classifier: '',
               file: "target/${mavenPom.artifactId}-${mavenPom.version}.${mavenPom.packaging}",
                type: "${mavenPom.packaging}"]],
                 credentialsId: 'nexusID',
                  groupId: "${mavenPom.groupId}",
                   nexusUrl: '192.168.33.10:8081',
                    nexusVersion: 'nexus3',
                     protocol: 'http',
                      repository: 'biom1',
                       version: "${mavenPom.version}"
            }           
        }
    }
   } 
}   