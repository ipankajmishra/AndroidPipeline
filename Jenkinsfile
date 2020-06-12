pipeline {
           agent any
           stages {
                stage("Git checkout") {
                     steps {
                          git "https://github.com/ipankajmishra/AndroidPipeline.git"
                     }
                }
                stage("Unit tests") {
                    steps{
                        bat 'gradlew test'
                    }
                }
                stage('Static Code Analysis') {
                    steps{
                        bat 'gradlew lint'
                    }
                }
                stage("Build") {
                    steps {
                        bat 'gradlew clean build -x test'
                    }
                }
                stage('Publish to App Center') {
                    environment {
                        APPCENTER_API_TOKEN = '7943fdb1a13850de26e5f7b67599c3ff87a90cc5'//'bde0c2278c1177b8cbf9ffc34dc106ce7da66b24'
                    }
                    steps {
                        appCenter apiToken: APPCENTER_API_TOKEN, 
                        appName: 'My-Application',
                        distributionGroups: 'Collaborators, Testers', 
                        ownerName: 'pankajmishra', 
                        pathToApp: 'app/build/outputs/apk/debug/app-debug.apk'
                    }
                }
           }
      }
