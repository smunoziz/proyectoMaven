pipeline {
    
    agent any
    
    stages {
        stage("Compilación") {
            sh "mvn compile"
        }
        stage("Pruebas") {
            stages {
                stage("Pruebas Dinámicas") {
                    /* Solucion con MAGIA... evitar                    
                    steps {
                        // Compilar pruebas -> Las pruebas no pueden ejecutarse
                        // Ejecutar pruebas -> Genera informe... tanto si se ejecutan bien como si se ejecutan mal
                    }
                    post {
                        always {
                            junit allowEmptyResults: true, testResults: 'target/surefire-reports/*.xml' 
                        }    
                    }
                    */                    
                    stages {
                        stage("Compilación pruebas") {
                            steps {
                                // Compilar pruebas -> Las pruebas no pueden ejecutarse
                                sh "mvn test-compile"
                            }
                        }
                        stage("Ejecución pruebas") {
                            steps {
                                // Ejecutar pruebas -> Genera informe... tanto si se ejecutan bien como si se ejecutan mal
                                sh "mvn test"
                            post{
                                always {
                                    junit testResults: 'target/surefire-reports/*.xml' 
                                }    
                            }
                        }
                    }
                }
                stage("SonarQube") {
                    sh """
                    mvn sonar:sonar -Dsonar.projectKey=proyectoMaven \
                    -Dsonar.host.url=http://172.31.14.158:8081 \
                    -Dsonar.login=429d6a159392f3a17187a1c6421f44d5d369c1b1
                    """
                }
            }
        }
        stage("Empaquetado") {
            steps {
                sh "mvn package -Dmaven.test.skip=true"
            }
            post{
                success {
                    archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false
                }
            }
        }
    }
    post {
        always {
            cleanWs deleteDirs: true, patterns: [[pattern: 'target', type: 'INCLUDE']]
        }
    }
}