pipeline {
    agent any
environment {
    VERSION = readMavenPom().getVersion()
}
    stages {
	stage('test') {
	    steps {
		echo "no junit or intergration tests"
	    }
	}
        stage('Build') {
            steps {
		    sh 'mvn package -DskipTests'
		    sh 'docker build -t="casestudiesnbs/spring-boot-backend:${VERSION}" .'
            }
        }
        stage('Deploy') {
            steps {
                    sh 'docker push casestudiesnbs/spring-boot-backend:${VERSION}'
            }
        }
        stage('Testing Environment') {
            steps {
                echo "API Tests not found"
            }
        }
        stage('Staging') {
          when{
              expression{
              env.BRANCH_NAME=='staging'
              }
          }
            steps {
                sh 'docker-compose pull'
                sh 'PROFILE=staging docker-compose up -d'
                sh 'mvn test -Dtest=SeleniumSuite'
            }
        }
        stage('Production') {
            when{
                expression{
                env.BRANCH_NAME=='master'
                }
            }
            steps {
                sh 'docker-compose pull'
                sh 'PROFILE=production docker-compose up -d'
                echo "Production"
            }
        }
    }
}
