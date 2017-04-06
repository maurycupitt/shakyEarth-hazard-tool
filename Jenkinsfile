#!usr/bin/env groovy

node {
stage('Testing') {
            notify('Testing')
            echo 'Testing'
        }

        stage('Staging') {
            notify('Staging')
            echo 'Staging'
        }

        stage('Deploy') {
            notify('Deploy')
            echo 'Deploying'
        }
} 


def notify (stage) {
  def postBody = '{ "summary": "' + stage + '"}'

  def response = httpRequest acceptType: 'APPLICATION_JSON', contentType: 'APPLICATION_JSON', httpMode: 'POST', requestBody: postBody, url: "http://172.16.240.189:8080/api/v1/artifacts/generic-gateway"
  
  echo("Status: "+response.status)
  echo("Content: "+response.content)
  
}
