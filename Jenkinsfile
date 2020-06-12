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
                stage("Build") {
                    steps {
                        bat 'gradlew clean build -x test'
                    }
                }
                      stage('Static Code Analysis') {
                    steps{
                        //bat 'gradlew lint'
                        appscan application: '75d946aa-1f67-4f74-a4c3-dc9e9341d28f',
                                   credentials: 'HCL APP SCAN', name: 'HCL APP SCAN',
                                   scanner: mobile_analyzer(hasOptions: false, target: 'C:\Program Files (x86)\Jenkins\workspace\My First Android Pipeline\app\build\outputs\apk\debug\app-debug.apk'),
                                   type: 'Mobile Analyzer'
                    }
                }
               /* stage('Publish to App Center') {
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
                }*/
           }
      }
