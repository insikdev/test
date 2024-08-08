pipeline {
  agent {
    label "jenkins"
  }

  triggers {
    pollSCM('* * * * *')  
  }

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', 
        url: 'https://github.com/insikdev/test'
      }
    }

    stage('Build') {
      steps {
        sh '/usr/lib/jvm/java-17-openjdk-amd64//bin/java -cp /var/lib/jenkins/plugins/maven-plugin/WEB-INF/lib/maven35-agent-1.14.jar:/usr/share/maven/boot/plexus-classworlds-2.x.jar:/usr/share/maven/conf/logging jenkins.maven3.agent.Maven35Main /usr/share/maven /var/cache/jenkins/war/WEB-INF/lib/remoting-3206.vb_15dcf73f6a_9.jar /var/lib/jenkins/plugins/maven-plugin/WEB-INF/lib/maven35-interceptor-1.14.jar /var/lib/jenkins/plugins/maven-plugin/WEB-INF/lib/maven3-interceptor-commons-1.14.jar 46101'
      }
    }

    stage('Test') {
      steps {
        sh 'echo run test'
      }
    }

    stage('Deploy') {
      steps {
        deploy adapters: [
            tomcat9(credentialsId: 'tomcat-manager', url: 'http://192.168.56.102:8080/')
          ], 
          contextPath: null, 
          war: 'target/hello-world.war'
          }     
      }   
  }
}
