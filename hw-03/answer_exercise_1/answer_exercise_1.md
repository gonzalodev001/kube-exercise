1A Creamos los objetos de forma declarativa, creamos el namespace part-second,
   el deployment.yaml, el service.yaml para exponer el servicio en el puerto 80,
   el ingress.yaml para acceder a través de la URL gonzalo.student.lasalle.com
   ejecutamos los siguientes comandos:

   - $ kubectl apply -f deployment.yaml
     $ kubectl apply -f service.yaml
     $ kubectl apply -f Ingress.yaml
     Verificamos que al ingress se le asigne el IP ADDRESS, una vez verificado
     añadimos la IP ADDRESS y la URL al host en la carpeta /etc/host como se
     observa la imagen, y con eso ya accedemos a la página de Nginx a través
     de la URL gonzalo.student.lasalle.com, resultado en la imagen. 

1B Creamos el certificado con la herramienta openssl con el siguiente comando

     - $ openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout tls.key -out tls.crt 
         -subj "/CN=gonzalo.student.lasalle.com"
     Después creamos el secret para el certificado con el siguiente comando.
      $ kubectl create secret tls nginx-secret-tls --cert=tls.crt --key=tls.key -n part-second
     Una vez hecho esto, añadimos a nuestro Ingress.yaml  el secretName y el hosts, 
     luego accedemos al navegador con la URL para verificar como se muestra en la imagen.