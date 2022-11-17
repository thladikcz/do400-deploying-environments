pipeline {

 agent {

 node {

 label 'maven'

 }

 }

 stages {

 stage('Tests') {

 steps {

 sh './mvnw clean test'

 }

 }

 stage('Package') {

 steps {

 sh '''

 ./mvnw package -DskipTests -Dquarkus.package.type=uber-jar

 '''

 archiveArtifacts 'target/*.jar'

 }

 }
stage('Build Image') {


 steps {

 sh '''

 ./mvnw quarkus:add-extension -Dextensions="kubernetes,container-image-jib"

 '''

 sh '''

 ./mvnw package -DskipTests -Dquarkus.jib.base-jvm-image=quay.io/redhattraining/do400-java-alpineopenjdk11-jre:latest -Dquarkus.container-image.build=true -Dquarkus.container-image.registry=quay.io -Dquarkus.container-image.group=thladik -Dquarkus.container-image.name=do400-deploying-environments -Dquarkus.container-image.username=thladik -Dquarkus.container-image.password="Most33fast1990" -Dquarkus.container-image.push=true

 '''

 }

}
 }

}
