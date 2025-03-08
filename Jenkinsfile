pipeline {
    agent any
    tools {
        jdk 'jdk17'
        maven 'maven3'
    }
    
    environment{
        SCANNER_HOME= tool 'sonar-tool'
    }

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/mob50/FullStack-Blogging-App.git'
            }
        }
        
        
        stage('Compile') {
            steps {
                sh 'mvn compile'
            }
        }
        
        
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }        
        
        stage('Trivy FS Scan') {
            steps {
                sh 'trivy fs --format table -o fs.html .'
            }
        }        
        
        
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonar-server') {
                sh '''$SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=Blogging-app -Dsonar.projectKey=Blogging-app \
                -Dsonar.java.binaries=target'''
}
            }
        }        
        
        
        stage('Build') {
            steps {
                sh 'mvn package'
            }
        }        
        
        
        stage('Publish to Nexus') {
            steps {
                withMaven(globalMavenSettingsConfig: 'maven-global', jdk: 'jdk17', maven: 'maven3', mavenSettingsConfig: '', traceability: true) {
                    sh 'mvn deploy'
}
            }
        }        
        
                
        stage('Build Image & Tag') {
            steps {
                script{
                withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                sh 'docker build -t vkedar/bloggingapp:latest .'    
                    }    
                }
            }
        }        
        
        stage('Trivy Image Scan') {
            steps {
                sh 'trivy image --format table -o image.html vkedar/bloggingapp:latest'
            }
        }        
        
        stage('Docker Image Push') {
            steps {
                
                script{
                withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                sh 'docker push vkedar/bloggingapp:latest'    
                    }    
                }
                
            }
        }        
        

        
        stage('k8s Deploy') {
            steps {
                
            withKubeConfig(caCertificate: '', clusterName: 'blogging-cluster', contextName: '', credentialsId: 'k8s-cred', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://EA18576996DE3EDC9A8D47126384EBDE.gr7.ap-south-1.eks.amazonaws.com') {
                sh 'kubectl apply -f deployment-service.yml'
}
                
            }
        }        
        
        
        stage('k8s Verify') {
            steps {
                
            withKubeConfig(caCertificate: '', clusterName: 'blogging-cluster', contextName: '', credentialsId: 'k8s-cred', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://EA18576996DE3EDC9A8D47126384EBDE.gr7.ap-south-1.eks.amazonaws.com') {
                sh 'kubectl get pods'
                sh 'kubectl get svc'
}
                
            }
        }        

        
       stage('6') {
            steps {
                echo "$SCANNER_HOME/bin/sonar-scanner"
            }
        }                
        
        
       stage('7') {
            steps {
                echo "$SCANNER_HOME/bin/sonar-scanner"
            }
        }                
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
    }
}
