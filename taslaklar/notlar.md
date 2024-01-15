apiVersion: apps/v1
kind: Deployment
metadata:
  name: mysql-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      name: msql-db
  template:
    metadata:
      labels:
        name: msql-db
    spec:
      containers:
      - image: mysql:5.7
        name: msql-db
        env:
        - name: MYSQL_ROOT_PASSWORD
          value: R1234r
        - name: MYSQL_DATABASE
          value: phonebook
        - name: MYSQL_USER
          value: clarus
        - name: MYSQL_PASSWORD
          value: Clarusway_1
        ports:
        - containerPort: 3306
        volumeMounts:
          - name: mysql-storage
            mountPath: /var/lib/mysql
      volumes:
        - name: mysql-storage
          persistentVolumeClaim:
            claimName: proje-pv-claim