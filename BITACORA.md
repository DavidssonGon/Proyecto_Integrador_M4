# BITACORA DEL PROYECTO INTEGRADOR DEL MODULO 04

Paso #1: Descargar el repositirio de github.
```
  git clone https://github.com/lopezdar222/herramientas_big_data
```

Paso #2: Entrar a "herramientas_big_data" y levantar el contenedor.
```
  cd herramientas_big_data
  sudo docker-compose -f docker-compose-v1.yml up -d
```

## 1) HDFS
Paso #3: Entrar al contenedor y crear directorio Datasets en el contenedor namenode.
```
  sudo docker exec -it namenode bash
  cd home
  mkdir Datasets
  exit
```

Paso #4: Copiar archivos a Datasets dentro del contenedor.
```
  sudo docker cp /home/ubuntu/herramientas_big_data/Datasets/calendario/Calendario.csv namenode:/home/Datasets/Calendario.csv
  sudo docker cp /home/ubuntu/herramientas_big_data/Datasets/canaldeventa/CanalDeVenta.csv namenode:/home/Datasets/CanalDeVenta.csv
  sudo docker cp /home/ubuntu/herramientas_big_data/Datasets/cliente/Cliente.csv namenode:/home/Datasets/Cliente.csv
  sudo docker cp /home/ubuntu/herramientas_big_data/Datasets/compra/Compra.csv namenode:/home/Datasets/Compra.csv
  sudo docker cp /home/ubuntu/herramientas_big_data/Datasets/empleado/Empleado.csv namenode:/home/Datasets/Empleado.csv
  sudo docker cp /home/ubuntu/herramientas_big_data/Datasets/gasto/Gasto.csv namenode:/home/Datasets/Gasto.csv
  sudo docker cp /home/ubuntu/herramientas_big_data/Datasets/producto/Producto.csv namenode:/home/Datasets/Producto.csv
  sudo docker cp /home/ubuntu/herramientas_big_data/Datasets/proveedor/Proveedor.csv namenode:/home/Datasets/Proveedor.csv
  sudo docker cp /home/ubuntu/herramientas_big_data/Datasets/sucursal/Sucursal.csv namenode:/home/Datasets/Sucursal.csv
  sudo docker cp /home/ubuntu/herramientas_big_data/Datasets/tipodegasto/TiposDeGasto.csv namenode:/home/Datasets/TiposDeGasto.csv
  sudo docker cp /home/ubuntu/herramientas_big_data/Datasets/venta/Venta.csv namenode:/home/Datasets/Venta.csv
  sudo docker cp /home/ubuntu/herramientas_big_data/Datasets/iris.csv namenode:/home/Datasets/iris.csv
  sudo docker cp /home/ubuntu/herramientas_big_data/Datasets/iris.json namenode:/home/Datasets/iris.json
  sudo docker cp /home/ubuntu/herramientas_big_data/Datasets/personal.csv namenode:/home/Datasets/personal.csv
  sudo docker cp /home/ubuntu/herramientas_big_data/Datasets/raw-flight-data.csv namenode:/home/Datasets/raw-flight-data.csv
```

Paso #5: Crear el directorio en HDFS llamado "/data".
```
  sudo docker exec -it namenode bash # Para entrar al contenedor

  hdfs dfs -mkdir -p /data
```

Paso #6: Copiar los archivos csv del directorio Datsets a HDFS.
```
  hdfs dfs -put /home/Datasets/* /data
```

## 2) Hive

Paso #7: Levantar el contenedor de HIVE.
```
  sudo docker-compose -f docker-compose-v2.yml up -d
```

Paso #8: Ingresar a HIVE desde la terminal.
```
  sudo docker exec -it hive-server bash
  hive
```

Paso #9: Pasar el script Paso02.hql al contendor con container ID.
```
  sudo docker cp /home/ubuntu/herramientas_big_data/Paso02.hql 2e0ba8809dc5:/opt/Paso02.hql
```

Paso #10: Crear las tablas desde la terminal ejecutando el script Paso02.hql.
```
  hive -f Paso02.hql
```

## 3) Formatos de Almacenamiento

Paso #11: Pasar el script Paso03.hql al contendor con el container ID.
```
  sudo docker cp /home/ubuntu/herramientas_big_data/Paso03.hql 2e0ba8809dc5:/opt/Paso03.hql
```

Paso #12: Ejecutar el script para alamcenarlas en formato ormato Parquet + Snappy además de de aplicar particiones para alguna de las tablas.
```
  hive -f Paso03.hql
```

## 4) SQL

Paso #13: Pasar los scripts Paso04.hql y Paso04_ConConsulta.hql al contendor con el container ID.
```
  sudo docker cp /home/ubuntu/herramientas_big_data/Paso04.hql 2e0ba8809dc5:/opt/Paso04.hql
  sudo docker cp /home/ubuntu/herramientas_big_data/Paso04_ConConsulta.hql 2e0ba8809dc5:/opt/Paso04_ConConsulta.hql
```

Paso #14: Ejecutar los scripts para crear índices en alguna de las tablas cargadas y probar los resultados.
```
  hive -f Paso04.hql
  hive -f Paso04_ConConsulta.hql
```
## 5) No-SQL

Paso #15: Levantar el contenedor de No-SQL.
```
  sudo docker-compose -f docker-compose-v3.yml up -d
```

#### 1) HBase:

Paso #16: Ingresar al contendeor ejecuntando HBASE
```
  sudo docker exec -it hbase-master hbase shell
```