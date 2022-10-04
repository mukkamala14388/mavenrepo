pipeline{
agent {label 'dev'}
triggers {
        pollSCM '* * * * *'
    }
stages{
stage('git checkout'){
steps{
checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: '0185d536-b101-4155-b03c-9e5c8e16e6db', url: 'https://github.com/mukkamala14388/mavenrepo.git']]])
}
}
stage('build'){
steps{
sh 'mvn package'
}
}
stage('sonar'){
steps{
withSonarQubeEnv('SonarQube') {
    sh 'mvn sonar:sonar'
}
}
}
stage('nexus'){
steps{
sh 'mvn deploy'
}
}
stage('tomcat'){
steps{
sh 'scp /root/workspace/GitIntegration/target/studentapp-2.1.1-FEAT01-SNAPSHOT.war 54.158.12.13:/var/lib/tomcat/webapps'
}
}
}
}
