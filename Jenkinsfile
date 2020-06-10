pipeline {
  agent any
  stages {
    stage('Build') {
      agent any
      steps {
        git(url: 'https://github.com/dinesh99088/offers', branch: 'master', changelog: true, poll: true)
        sh 'mvn compile test package'
      }
    }

    stage('Place jar file') {
      agent {
        node {
          label 'Ansible_Agent'
        }

      }
      steps {
        ws(dir: '/opt/copy_jar')
        git(url: 'https://github.com/dinesh99088/CICD_With_Ansible', branch: 'DEV-Ansible', changelog: true, poll: true)
        sh 'ansible-playbook copy.yml'
      }
    }

    stage('Run jar file') {
      agent {
        node {
          label 'Tomcat_Agent'
        }

      }
      steps {
        fileExists '/home/tomcat/apache-tomcat-8.5.55/webapps/offers-0.1.0.jar'
        echo '"Work done"'
      }
    }

  }
}