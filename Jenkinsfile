#!usr/bin/env groovy

stage("Notify") {
  def response = httpRequest 'http://172.16.240.189:8080/api/v1/artifacts/generic-gateway'
        println("Status: "+response.status)
        println("Content: "+response.content)
  echo 'Mara'
}
