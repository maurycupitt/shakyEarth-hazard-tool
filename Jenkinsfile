#!usr/bin/env groovy

node {
stage('Testing') {
            notify('Testing', "${env.JOB_NAME}", "${env.BUILD_NUMBER}")
            echo ('Testing') 
            echo "${env.JOB_NAME}"
            echo "${env.BUILD_NUMBER}"
            echo sh(returnStdout: true, script: 'env')
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
  def postBody = '{ "formatted_id": "' + job_name +  \
            '","summary": "' + stage + ' - ' + job_name + ' - ' + build_number +  \
            '","description": ' + stage +  \
            '","status": "Done", \
            "created": "2001-10-08T18:20:34.000+0000", \
            "location": "' + env.JOB_DISPLAY_URL + '", \
            "scm_revision": "String", \
            "scm_url": "http://example.com" \
            }'
  echo postBody

  def response = httpRequest acceptType: 'APPLICATION_JSON', contentType: 'APPLICATION_JSON', httpMode: 'POST', requestBody: postBody, url: "http://172.16.240.189:8080/api/v1/artifacts/build-results"
  
  echo("Status: "+response.status)
  echo("Content: "+response.content)
  
}
