3 Para realizar la prueba de metricas HPA debemos activar en minikube
  el addon metrics-server, depués creamos el objeto deployment, su
  servicio para acceder, crear el objeto hpa con las reglas de un mínimo
  de replicas de 1 y un máximo de replicas a 10, que es entre esta cantidad
  de replicas para que funcione el hpa, luego temos el recurso del cpu 
  utilizada al 50%.

  Una vez creados nuestros obejtos, verificamos al inico que el uso de cpu es 0%,
  al hacer tráfico a nuestro servicio depués de un tiempo vemos que empieza a hacer 
  el uso del cpu 146% superando la asignada en nuestra relga en hpa. 
  
  - $ kubectl run -i --tty load-generator --rm --image=busybox --restart=Never --
    >> /bin/sh -c "while sleep 0.01; do wget -q -O- http://192.168.99.100:30000/; done"
  
   
  De esta forma empieza a escalar los pods a un número de 3 para mantener esa regla, 
  al cancelar el tráfico pasados unos minutos desescala los pods a 1.
  Podemos observar los resultados en las imágenes.