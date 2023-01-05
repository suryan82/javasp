node {
    stage('Git Clone'){
        git branch: 'main', credentialsId: 'GIT-CREDENTIALS', url: 'https://github.com/manash6173/maven-web-app.git'
    }
    stage('Maven Build'){
        def mavenHome = tool name: "Maven-3.8.6", type: "maven"
        def mavenCMD = "${mavenHome}/bin/mvn"
        sh "${mavenCMD} clean package"
    }
    stage('Sonar Analysics'){
        withSonarQubeEnv('Sonar-Server-7.8') {
			def mavenHome = tool name: "Maven-3.8.6", type: "maven"
			def mavenCMD = "${mavenHome}/bin/mvn"
			sh "${mavenCMD} sonar:sonar"
        }
    }
    stage('Deploy to Tomcat Server'){
        deploy adapters: [tomcat9(credentialsId: 'TOMCAT-CREDENTIALS', path: '', url: 'http://13.127.37.238:8080/')], contextPath: '/app', war: 'target/maven-web-app.war'
    }
}
