pipeline {
  agent any
  stages {
    stage('checkout') {
      steps {
        git(url: 'git@github.com:gjagadish473/pipeline-one.git', branch: 'main')
      }
    }

    stage('build') {
      steps {
        sh '/opt/maven38/bin/mvn clean package'
      }
    }

    stage('upload') {
      steps {
        sh 'aws s3 cp target/petclinic.war s3://dev-jrtechee-artifactory/petclinic-$BUILD_NUMBER.war'
      }
    }

    stage('deploy') {
      steps {
        sh 'aws s3 cp s3://dev-jrtechee-artifactory/petclinic-$BUILD_NUMBER.war petclinic.war scp petclinic.war root@10.0.99.210:/opt/tomcat/webapps/'
      }
    }

  }
}