¿Cúal sería el comando que utilizarías para escalar el número de replicas a
10?
    - Crear objeto de tipo replicaSet, debe tener 3 replicas
     $ kubectl create -f ./PodReplicas.yaml

    - Con el siguiente comando indicamos para escalar scale, --replicas=10 
      el número de replicas que queremos, de tipo replicaset y el nombre de nuestro pod.
    $ kubectl scale --replicas=10 replicaset nginx-server-replicaset

Si necesito tener una replica en cada uno de los nodos de Kubernetes,
¿qué objeto se adaptaría mejor?

    - Para que se cumpla tener una replica en cada uno de los nodos se necesita crear
      un obejto de tipo DaemonSet
