pipeline {
    agent {
        label "swarm"
    }
    stages {
        stage('preparing docker') {
            agent {
                docker { 
                    image 'gradle:6.3.0-jdk8'
                    args '--entrypoint=\'\' -v ${PWD}:/usr/src/app -w /usr/src/app'
                    reuseNode true
                }
            }
            stages {
                stage ('Install') {
                    steps {
                        script {
                            sh './gradlew assembleDebug'
                        }
                    }
                }
                // stage ('Analyzing with SonarQube') {
                //     steps {
                //         sh 'mvn -DskipITs --settings ./maven/settings.xml sonar:sonar'
                //     }
                // }
                // stage('Building binary') {
                //     steps {
                //         script {
                //             sh 'mvn -DskipITs --settings ./maven/settings.xml clean package'
                //             sh 'cp -r target/ src/'
                //         }
                //         step([$class: 'TeamCollectResultsPostBuildAction'])
                //     }
                //     post {
                //         always {
                //             archiveArtifacts artifacts: 'target/*.apk, *.sql', onlyIfSuccessful: true
                //         }
                //     }
                // }
            }
        }
        // stage('Deploy for production') {
        //     when {
        //         branch 'master'
        //     }
        //     stages {
        //         stage('Building image') {
        //             steps{
        //                 script {
        //                     dockerImage = docker.build registry + ":v1.0.$BUILD_NUMBER", "./src"
        //                     dockerImage = docker.build registry + ":latest", "./src"
        //                 }
        //             }
        //         }
        //         stage('Deploy Image') {
        //             steps{
        //                 script {
        //                     docker.withRegistry( '', registryCredential ) {
        //                         dockerImage.push()
        //                     }
        //                 }
        //             }
        //         }
        //         stage('Remove Unused docker image') {
        //             steps{
        //                 sh "docker rmi $registry:v1.0.$BUILD_NUMBER"
        //                 sh "docker rmi $registry:latest"
        //             }
        //         }
        //     }
        // }
        stage('Clean') {
            steps {
                deleteDir()
            }
        }
    }
}