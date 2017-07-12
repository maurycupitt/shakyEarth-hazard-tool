#!usr/bin/env groovy

node {
    stage('Testing') {
            notify('Testing', "${env.JOB_NAME}", "${env.BUILD_NUMBER}")
            echo ('Testing') 
            echo "${env.JOB_NAME}"
            echo "${env.BUILD_NUMBER}"
            echo sh(returnStdout: true, script: 'env')
        }
    stage('SonarQube analysis') { 
        withSonarQubeEnv('Sonar') { 
          sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.3.0.603:sonar ' + 
          '-f all/pom.xml ' +
          '-Dsonar.projectKey=com.huettermann:all:master ' +
          '-Dsonar.login=$SONAR_UN ' +
          '-Dsonar.password=$SONAR_PW ' +
          '-Dsonar.language=java ' +
          '-Dsonar.sources=. ' +
          '-Dsonar.tests=. ' +
          '-Dsonar.test.inclusions=**/*Test*/** ' +
          '-Dsonar.exclusions=**/*Test*/**'
        }
    }
    stage("SonarQube Quality Gate") { 
        timeout(time: 1, unit: 'HOURS') { 
           def qg = waitForQualityGate() 
           if (qg.status != 'OK') {
             error "Pipeline aborted due to quality gate failure: ${qg.status}"
           }
        }
    }

        stage('Staging') {
            notify('Staging', "${env.JOB_NAME}", "${env.BUILD_NUMBER}")
            echo 'Staging'
        }

        stage('Deploy') {
            notify('Deply', "${env.JOB_NAME}", "${env.BUILD_NUMBER}")
            echo 'Deploying'
        }
} 


def notify (stage, job_name, build_number) {
  def rightNow = new Date().format("yyyy-MM-dd'T'HH:mm:ss'Z'", TimeZone.getTimeZone("UTC")) 
  def postBody = '{ "formatted_id": "' + job_name +  \
            '","summary": "' + stage + ' - ' + job_name + ' - ' + build_number +  \
            '","description": ' + stage +  \
            '","status": "Done", \
            "created": "' + rightNow + '", \
            "location": "' + env.JOB_DISPLAY_URL + '", \
            "scm_revision": "String", \
            "scm_url": "' + env.RUN_DISPLAY_URL + '" \
            }'
  echo postBody

  def response = httpRequest acceptType: 'APPLICATION_JSON', contentType: 'APPLICATION_JSON', httpMode: 'POST', requestBody: postBody, url: "http://172.16.241.20:8080/api/v1/artifacts/inbound-builds"
  
  echo("Status: " + response.status)
  echo("Content: " + response.content)
  
}
