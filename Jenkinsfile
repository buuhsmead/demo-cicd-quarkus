#!groovy

node("maven") {

    stage("SCM checkout") {
        def commitHash = checkout(scm).GIT_COMMIT

        // debug printje
        print(commitHash)
    }


    // define maven with custom settings.xml (using this path as convention.. define a env var if desired...)
    // def mvnCmd = "mvn -s ${WORKSPACE}/maven/settings.xml"
    def mvnCmd = "mvn"

    stage("Build the Frontend JAR") {

        dir('maven') {

            dir('frontend') {
                sh "ls -ltr"

                // run the application in dev mode using: mvn compile quarkus:dev
                //   sh "${mvnCmd} compile quarkus:dev"
                // run the generated app
                //  java -jar getting-started-0.1.0-SNAPSHOT-runner.jar
                // mvn clean package test
                sh "${mvnCmd} package test"

            }
        }

    }

    stage("Unit Testing & Analysis") {

        echo "Using sonar at url ${params.SONAR_URL}"
        echo "Tijdelijk niet actief."

//        dir('maven') {
//            dir('frontend') {
//                parallel(
//                        'Test': {
//                            sh "${mvnCmd} test"
//                            step([$class: 'JUnitResultArchiver', testResults: '**/target/surefire-reports/TEST-*.xml'])
//                        },
//                        'Static Analysis': {
//                            sh "${mvnCmd} mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.6.0.1398:sonar -Dsonar.host.url=${params.SONAR_URL} -DskipTests=true"
//                        }
//                )
//            }
//        }
    }


    stage("Push artifact to Nexus") {

        echo "Pushing artifact to Nexus at url ${params.NEXUS_URL}"

        echo "Tijdelijk niet actief."
//        dir('maven') {
//            dir('frontend') {
//                // deploy
//                sh "${mvnCmd} deploy -Dnexus.url=${params.NEXUS_URL}"
//                // extract info from pom.xml to build NEXUS_ARTIFACT_PATH
//                def pom = readMavenPom file: "pom.xml"
//                // global variable
//                APP_VERSION = pom.version
//                def artifactId = pom.artifactId
//                def groupId = pom.groupId.replace(".", "/")
//                def packaging = pom.packaging
//                NEXUS_ARTIFACT_PATH = "${groupId}/${artifactId}/${APP_VERSION}/${artifactId}-${APP_VERSION}.${packaging}"
//            }
//        }

    }


    stage('Native Build') {

        dir('maven') {
            dir('frontend') {
               sh "${mvnCmd} package -Pnative -Dnative-image.docker-build=true"
            }
        }
    }


}
