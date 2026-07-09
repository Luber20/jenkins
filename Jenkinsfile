pipeline {
    agent any

    tools {
        nodejs "Node16" 
        dockerTool 'Dockertool'  // <-- Aquí está la corrección (dockerTool)
    }

    stages {
        stage('Pruebas Automáticas') {
            steps {
                // Instala las herramientas de prueba en Jenkins
                sh 'npm install'
                // Ejecuta las pruebas
                sh 'npm test'
            }
        }

        stage('Construir Imagen Docker') {
            steps {
                sh 'docker build -t hola-mundo-node:latest .'
            }
        }

        stage('Ejecutar Contenedor Node.js') {
            steps {
                sh '''
                    # Detener y eliminar cualquier contenedor previo
                    docker stop hola-mundo-node || true
                    docker rm hola-mundo-node || true

                    # Ejecutar el contenedor de la aplicación
                    docker run -d --name hola-mundo-node -p 3000:3000 hola-mundo-node:latest
                '''
            }
        }
    }
}
