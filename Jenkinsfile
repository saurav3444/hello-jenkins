pipeline {
    agent any

    tools {
        maven 'Maven-3.6.3'
    }

    stages {
        stage("Test") {
            steps {
                sh "mvn clean test"
            }
        }

        stage("Build") {
            steps {
                sh "mvn package -DskipTests"
            }
        }

        stage("Execute Main class") {
            steps {
                sh "java -cp target/hello-jenkins-1.0-SNAPSHOT.jar com.sapient.Main \"Saurav Kumar\""
            }
        }

    }
  post {
        always {
            echo "This will always be executed"
        }
        success {
            echo "This will be executed only when all stages succeed"
            junit '**/*xml'
            archiveArtifacts artifacts: "target/${JAR_FILENAME}-${JAR_VERSION}.jar", followSymlinks: false

        }
        failure {
            echo "This will be executed whenever any stage fails"
        }
    }

    
}
