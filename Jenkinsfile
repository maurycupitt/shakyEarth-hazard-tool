#!usr/bin/env groovy

stage("Notify") {
  def response = httpRequest 'http://localhost:8085/jenkins/api/json?pretty=true'
        println("Status: "+response.status)
        println("Content: "+response.content)
  echo 'Mara'
}
