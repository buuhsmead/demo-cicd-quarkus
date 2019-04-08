#!groovy

node("maven") {

    stage("SCM checkout") {
        def commitHash = checkout(scm).GIT_COMMIT
    }


    // define maven with custom settings.xml (using this path as convention.. define a env var if desired...)
    // def mvnCmd = "mvn -s ${WORKSPACE}/maven/settings.xml"
    def mvnCmd = "mvn"

    stage("Build Frontend") {
        sh "ls -ltr"

        sh "${mvnCmd} compile quarkus:dev"

    }


}
