pipeline {
    agent any
    stages { 
        stage('Example') {
            steps {
                when { changeRequest target: 'master' }
                echo 'Hello World'
            }
        }
    }
}
