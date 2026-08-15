# Jenkins + Docker

Repositorio de práctica para desplegar una página web estática con Nginx, Docker y Jenkins.

## Datos de la práctica

- Nombre completo: Angel Daniel Chalì Cajbòn
- Carné: 4090-22-1046
- Curso: Aseguramietno de la Calidad de Software
- Repositorio: https://github.com/Chali-17/jenkins-docker-Chali-Cajbon.git

## Archivos incluidos

- index.html
- Dockerfile
- Jenkinsfile
- README.md

## Construcción y prueba local

1. Construir la imagen Docker.

```bash
docker build -t jenkins-docker-chali-cajbon:1 .
```

2. Crear y publicar el contenedor en el puerto 8080.

```bash
docker run -d --name jenkins-docker-web -p 8181:80 jenkins-docker-chali-cajbon:1
```

3. Verificar en el navegador.

Abrir http://localhost:8080

4. Comprobar el contenedor en ejecución.

```bash
docker ps
```

5. Detener o eliminar el contenedor si se necesita repetir la prueba.

```bash
docker rm -f jenkins-docker-web
```

## Jenkins

Configurar un job llamado primerpipeline de tipo Pipeline con definición desde SCM y apuntando a la rama principal del repositorio.

El Jenkinsfile incluido en el repositorio implementa estas etapas:

1. Clonación del repositorio.
2. Verificación de index.html y Dockerfile.
3. Construcción de la imagen con el número de ejecución de Jenkins.
4. Despliegue del contenedor reemplazando el anterior si existe.
5. Confirmación del resultado.

## Procedimiento sugerido para las evidencias

1. Subir los archivos al repositorio GitHub.
2. Crear al menos tres commits con mensajes descriptivos.
3. Configurar Jenkins con el job primerpipeline.
4. Ejecutar el pipeline manualmente.
5. Tomar capturas del pipeline, consola, contenedor y aplicación.
6. Modificar index.html, subir el cambio y ejecutar otra vez el pipeline.
7. Confirmar que la aplicación refleje la actualización.

## Comandos útiles

```bash
git add .
git commit -m "Crear página web base"
git commit -m "Agregar Dockerfile con Nginx"
git commit -m "Agregar Jenkinsfile y documentación"
git remote add origin https://github.com/Chali-17/jenkins-docker-Chali-Cajbon.git
git branch -M main
git push -u origin main
```

## Notas

- La aplicación queda disponible en el puerto 8080 de la máquina local.
- El contenedor se llama jenkins-docker-web.
- La imagen se etiqueta con el número de ejecución de Jenkins.
