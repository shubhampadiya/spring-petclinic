 node {
           def mvnHome
      stage('Preparation') { // for display purposes
              // Get PetClinic code from a GitHub repository
              git 'https://github.com/mitesh51/spring-
         petclinic.git'
             // Get the Maven tool.
             // ** NOTE: This 'apache-maven-3.3.1' Maven tool must be 
             configured in the global configuration.
             mvnHome = tool 'apache-maven-3.3.1'
             }
            stage('SonarQube analysis') {
             // requires SonarQube Scanner 3.0+
            def scannerHome = tool 'SonarQube Scanner 3.0.3';
         // Sonarqube6.3 must be configured in the Jenkins
         Configuration -> Add SonarWube server 
                 withSonarQubeEnv('Sonarqube6.3') {
         //provide all required properties for Sonar execution
                     bat "${scannerHome}/bin/sonar-scanner -
         Dsonar.host.url=http://localhost:9000/ -
         Dsonar.login=1335c62cbfceab5
         954a5101ab7477cc974f58d56 -
         Dsonar.projectVersion=1.0
         -Dsonar.projectKey=petclinicKey -
         Dsonar.sources=src"
                 }
            } 
	stage('Build') {
                 // Run the maven build based on the Operating system
                 if (isUnix()) {
        sh "'${mvnHome}/bin/mvn' -
         Dmaven.test.failure.ignore clean package"
           // Publish JUnit Report
               junit '**/target/surefire-reports/TEST-*.xml'
               } else {
                  bat(/"${mvnHome}\bin\mvn" clean package/)
          // Publish JUnit Report
              junit '**/target/surefire-reports/TEST-*.xml'

              }
           }
         }
