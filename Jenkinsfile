#!usr/bin/env groovy

stage("Notify") {
  def postBody = """
    {"summary": "My summary"}
"""
def response = httpRequest acceptType: 'APPLICATION_JSON', contentType: 'APPLICATION_JSON', httpMode: 'POST', requestBody: postBody, url: "http://172.16.240.189:8080/api/v1/artifacts/generic-gateway"
  println("Status: "+response.status)
  println("Content: "+response.content)
  echo 'Mara'
}
