1A ¿Cómo puedo obtener las últimas 10 líneas de la salida estándar (logs
 generados por la aplicación)?

    -Ejecutando el comando siguiente, donde --tail le indicamos las últimas línea que queremos obtener.

    $ kubectl logs --tail=10 nginx-server-v1 

1B ¿Cómo podría obtener la IP interna del pod? Aporta capturas para indicar
 el proceso que seguirías.

    - Para obtener la IP interna del pod y que imprima por pantalla  podemos utilizar el siguiente comando:
	
    $ kubectl get pod nginx-server-v1 --template={{.status.podIP}} 

    otra alternativa listando los pods

    $ kubectl get pods -o wide

    donde lista la información detallada de todos los pods del namespaces default y nos mostrar las ips de los pods.

    <img src="hw-02/images/exercise_1/image_1B.png">

    O podemos con el siguiente comando que describe la inforación de un pod en especifico, que de igual manera 
    nos muestra su ip interna.

    $ kubectl describe pod nginx-server-v1

1C¿Qué comando utilizarías para entrar dentro del pod?

    - Ejecutamos el siguiente comando.

    $ kubectl exec -it nginx-server-v1 -- /bin/bash

1D Necesitas visualizar el contenido que expone NGINX, ¿qué acciones
 debes llevar a cabo?

    Para exponer utilizamos el comando port-forward para asignarle una ip 8080 para que sea accesible a nuestera pc.

    $ kubectl port-forward nginx-server-v1 8080:80

1E Indica la calidad de servicio (QoS) establecida en el pod que acabas de
 crear. ¿Qué lo has mirado?

    -para verificar la calidad de servicio que tiene el pod lanzamos el siguiente comando para ver de forma detallada el pod.

    $ kubectl get pod nginx-server-v1 -n default --output=yaml
    
    que nos mostrara un json con la información de las características del pod, donde nos muestra la calidad de servicio Qos
    que es Guaranteed (Garantizada) como se observa en la imagen, se encuentran en 
    kube-exercise/hw-02/images/exercise_1/
