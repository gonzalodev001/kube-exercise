¿Cúal sería el comando que utilizarías para escalar el número de replicas a
10?

    - Con el siguiente comando indicamos para escalar scale, --replicas=10 con esto indicamos
      el número de replicas que queremos, de tipo replicaset y el nombre de nuesto pod.
    $ kubectl scale --replicas=10 replicaset nginx-demo

Si necesito tener una replica en cada uno de los nodos de Kubernetes,
¿qué objeto se adaptaría mejor?

    - Para que se cumpla tener una replica en cada uno de los nodos se necetia crear
      un obejto de tipo DaemonSet