pipeline {
    agent any
    stages {
        stage('gitclone')
        {
            steps {
                echo "Cloning from GitHub"
                git 'https://github.com/rkgithub2020/spring3hibernate-1.git'
                  }
        }
        stage('clean')
            {
            steps {
                echo "Cleaning workspace"
                sh 'mvn clean'
            }
            }
stage('run-parallel-compile') {
  steps {
    parallel(
      a: {
        sh 'mvn compile'
      }
    )
  }
}
stage('run-parallel-Stability Ananlysis') {
  steps {
    parallel(
      a: {
        sh 'mvn "pmd:pmd"'
      },
      b: {
        sh 'mvn checkstyle:checkstyle'
      }
    )
  }
}
         stage('Code Build')
        {
            steps {
                echo "Building Code"
                sh 'mvn package'
                  }
         }
         stage('Code validate')
        {
            steps {
                echo "Building Code"
                sh 'mvn validate'
                  }
         }
        stage('Publish Report')
        {
            steps {
                publishCoverage adapters: [jacocoAdapter('**/checkstyle-result.xml')], sourceFileResolver: sourceFiles('NEVER_STORE')
        }
         }
    stage('Email Notification')
        {
            steps {
                echo "Sending Email notification"
                emailext body: '', subject: 'Pipeline Build Notification', to: 'anurag.gaurav@mygurukulam.org'
        }
    }
    stage('Slack Notification')
        {
            steps {
                echo "Sending Slack notification"
                slackSend channel: 'testingninja1202', failOnError: true, message: 'Pipeline Build notification', teamDomain: 'opstree', tokenCredentialId: 'b0ca748c-ef18-48ff-bd88-d628d52f4b59'
        }
        }
}
}
