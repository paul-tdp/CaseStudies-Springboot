pipeline {
    agent any

    stages {
        stage('Test') {
            steps {
                    echo "testing"
                }
            }
        stage('Build') {
            steps {
                echo "building"
                }
            }
        stage('Deploy') {
            steps {
                echo "hello"
            }
        }
          stage('Testing Environment') {
            steps {
                    echo "testing environment"
            }
        }
      stage('Staging') {
		when {
			expression {
				env.BRANCH_NAME == 'Developer'
			}
		}
            steps {
                echo "staging if in Developer branch"
            }
        }
      stage('Production') {
	when {
		expression {
			env.BRANCH_NAME == 'master'
		}
	}
            steps {
                echo "production if in master branch"
            }
        }
    
    }
}
