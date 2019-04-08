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

    stage("Build and Unit test the Frontend") {

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


}
