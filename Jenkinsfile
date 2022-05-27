pipeline{
    agent any
   /* tools{
        maven "maven3"
    } */
    environment {
        SNAP_REPO = "maven-snapshots"
        NEXUS_USER="admin"
        NEXUS_PASS="admin"
        RELEASE_REPO="ci-release"
        CENTRAL_REPO="maven-central1"
        NEXUS_GRP_REPO="maven-group"
        NEXUSIP = "3.93.88.165"
        NEXUSPORT = "8081"
    }
   stages{
       stage('Fetch code'){
           steps{
               git branch: 'jpac',
               url: 'https://github.com/Rahbna/ci-jenkins.git'
           }
       }
       stage('BUILD'){
            steps {
             sh'mvn install -DskipTests'
            }
        }
        stage('INTERGRATION'){
            steps {
             sh'mvn verify -DskipTests'
            }
        }
        stage('TEST'){
            steps {
             sh'mvn test'
            }
        }
        stage('Slack notif'){
            steps {
                slackSend channel: '#jenkins-slack',
                          message: 'Build and Tested successfully'
            }
        }
   }
}



