pipeline {
    agent any
    stages {
        stage ('compilation') {
            steps {
                sh 'mvn -B compile'
            }
        }
//        stage ('static code analysis') {
//            steps {
//                sh 'echo hello there. this  is static code analysis stub'
//                sh '/home/ubuntu/sonar-scanner-4.6.2.2472-linux/bin/sonar-scanner'
//            }
//        }
        stage ('package') {
            steps {
                sh 'mvn -B package'
            }
        }
 //       stage ('build and publish to dockerhub') {
 //           steps {
 //               sh 'sudo docker build -t devopsxprts/ab:latest .'
 //               sh 'sudo docker push devopsxprts/ab:latest'
 //           }
 //       }
        stage ('Deploy to tomcat1') {
            steps {
                sh 'scp target/addressbook-2.0.war tomcat@ip-172-31-10-165:/var/lib/tomcat9/webapps/addressbook.war'
            }
        }
        stage ('Deploy to tomcat 2') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://13.127.37.205:8080/')], contextPath: null, war: 'target/addressbook-2.0.war'
            }
        }

 //       stage ('deploy on kubernetes') {
//            agent { label "kubernetes" }
 //           steps {
//                sh 'kubectl apply -f https://raw.githubusercontent.com/upshiftnow/addressbook/master/deployment.yaml'
//                kubernetesDeploy configs: 'deployment.yaml', kubeconfigId: 'kube-config'
 //           }
  //      }
   }
    post {
        failure {
            sh 'echo the build failed'
        }
        success {
            sh 'echo the build is SUCCESSFULL'
        }
        always {
            sh 'echo the build as completed'
        }
    }
}
