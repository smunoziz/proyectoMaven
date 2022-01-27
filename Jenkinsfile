//Sintaxis declarativa MAS SENCILLA Y LA MAS USADA. Menos potente que la de scripting ... pero mucho mas que los proyectos de estilo libre.
//Sintaxis de scripting. MAS COMPLEJA Y MAS POTENTE: Puedo hacer lo que quiera con Jenkins.

pipeline {
    
    agent any // Para definir dónde quiero que se ejecute esta tarea.
    
    stages {
        
        stage("Etapa 1") {
           steps{ //Hacemos las llamadas a los plugins
              sh "echo Soy la etapa 1" //LLamada al plugin que ejecuta una shell
           } 
        }   
        
        stage("Etapa 2") {
            steps{
              sh """
              echo Soy la etapa 2
              echo Acabo la etapa 2
              """
           }
        }
    }
    
}
