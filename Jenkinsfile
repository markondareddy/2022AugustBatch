node{
    def mvnHome
    
    stage('scm'){
         git branch: 'master', credentialsId: 'spring-repo-credentials', url: 'https://github.com/markondareddy/spring-maven-hello-world.git'
    
         mvnHome= tool 'maven 3.8.6'
    }
    
     stage('clean'){
      sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore=true clean"
        
    }
    
    
    stage('build'){
      sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore=true package"
        
    }
    
    stage('Artifactfile'){
       archiveArtifacts 'target/*.war'
    }
    
    stage('deploy'){
       withCredentials([usernameColonPassword(credentialsId: 'tomcat_credential', variable: 'tomcat_credential')]) {
               sh "curl -v -u ${tomcat_credential} -T /var/lib/jenkins/workspace/declarative/target/CalculationMavenApp.war 'http://ec2-15-206-153-69.ap-south-1.compute.amazonaws.com:8080/manager/text/deploy?path=/CalculationMavenApp&update=true'"
               }
    }
    
    
}
