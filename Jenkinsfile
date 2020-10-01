pipeline {
    agent any
    stages { 
        stage('Example') {
            when { changeRequest target: 'master' }
            steps {          
               echo 'Hello World'
            }
        }
    }
}
