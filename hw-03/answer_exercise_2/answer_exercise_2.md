2 Creamos un statefulset con 3 instancias de mongoDB, junto a su servicio
  con el cluster ip none, con los siguientes comandos

    - $ kubectl apply -f mongodb-statefulset.yaml
      $ kubectl apply -f mongodb-service.yaml

  Luego ingresamos a el pod mongo-0 para habilitar el cluster de mongoDB

   - $ kubectl exec -it mongo-0 sh
  
  habilitamos el cluster con el siguiente comando.
   - > rs.initiate({_id: "rs0", version: 1, members: [
       { _id: 0, host : "mongo-0.mongodb-svc.default.svc.cluster.local:27017"},
       { _id: 1, host : "mongo-1.mongodb-svc.default.svc.cluster.local:27017"},
       {_id: 2, host : "mongo-2.mongodb-svc.default.svc.cluster.local:27017"}
       ]});

  Luego creamos un deployment de mongo-experss para hacer una operación en 
  una de las instancia mediante la UI de mongo express, y exponemos un servicio
  para acceder por el exterior.

    - $ kubectl apply -f mongo-express.yaml
      $ kubectl port-forward mongo-express-68f4d998-bhxrp 3000:8081
    
  Una vez realizada la operación de crear una base de datos y un objeto en
  mongo express verificamos ingresando a un pod en este caso en la 
  instancia mongo-1, para ver el cambio que se realizó, se puede apreciar 
  los resultados en las imagenes de captura.

    - $ kubectl exec -it mongo-1 sh
      rs0:SECONDARY> rs.secondaryOk()
      rs0:SECONDARY> show dbs
      rs0:SECONDARY> use university
      rs0:SECONDARY> show tables
      rs0:SECONDARY> db.students.find()
      { "_id" : ObjectId("60184277eb399400092d1b07"), "student" : "Gonzalo" }

La diferencia si se hubiera realizado con el objeto de ReplicaSet es que 
kubernetes les añade un hash aleatorio a cada instancia y si en algún momento
una instancia muere y este se vuelve a crear, pero lo haría con un diferente hash
y perdería los cambios realizados por esa razón es inconsiste hacer con Replicaset,
porque en el caso del obetjo statefulSet el pod se vuelve a crear con el mismo hash
que tenía asignado de forma ascendente.