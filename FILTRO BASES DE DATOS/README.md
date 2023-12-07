# FILTRO BASES DE DATOS

JEFFERSON DARIO BELTRAN LASPRILLA - Campuslands

### Creacion y poblacion de las tablas


```sql
   CREATE DATABASE METRO;
   USE METRO;

  	CREATE TABLE CONDUCTOR(
     ID_CONDUCTOR INT NOT NULL PRIMARY KEY,
     NOMBRE_CONDUCTOR VARCHAR(30),
     APELLIDO_CONDUCTOR VARCHAR(30));

    CREATE TABLE ZONA(
     ID_ZONA INT NOT NULL PRIMARY KEY, 
     NOMBRE_ZONA VARCHAR (15) );


    CREATE TABLE BUS(
        ID_BUS INT NOT NULL PRIMARY KEY,
        PLACA VARCHAR (8));


    CREATE TABLE RUTA(
        ID_RUTA INT NOT NULL PRIMARY KEY,
        NOMBRE_RUTA VARCHAR (20),
        TIEMPO TIME);


    CREATE TABLE ESTACIONES(
        ID_ESTACION INT NOT NULL PRIMARY KEY,
        NOMBRE_ESTACION VARCHAR (30));

    CREATE TABLE PROGRAMACION(
        ID_CONDUCTOR INT,
        ID_RUTA INT,
        ID_ZONA INT,
        ID_BUS INT,
        DIA VARCHAR(10));

    CREATE TABLE RUTA_X_ZONA(
         ID_ZONA INT,
         ID_RUTA INT);

    CREATE TABLE RUTA_X_ESTACION( 
        ID_RUTA INT, 
        ID_ESTACION INT);


```

### HAGO LOS ALTER NECESARIOS SEGUN MI PLANTEAMIENTO
```sql
ALTER TABLE PROGRAMACION ADD CONSTRAINT FK_PROGRAMACION_CONDUCTOR FOREIGN KEY (ID_CONDUCTOR) REFERENCES CONDUCTOR (ID_CONDUCTOR);

ALTER TABLE PROGRAMACION ADD CONSTRAINT FK_PROGRAMACION_RUTA  FOREIGN KEY (ID_RUTA) REFERENCES RUTA (ID_RUTA);

ALTER TABLE PROGRAMACION ADD CONSTRAINT FK_PROGRAMACION_ZONA  FOREIGN KEY (ID_ZONA) REFERENCES ZONA (ID_ZONA);

ALTER TABLE PROGRAMACION ADD CONSTRAINT FK_PROGRAMACION_BUS  FOREIGN KEY (ID_BUS) REFERENCES BUS (ID_BUS);

ALTER TABLE RUTA_X_ZONA ADD CONSTRAINT FK_RUTA_X_ZONA_ZONA  FOREIGN KEY (ID_ZONA) REFERENCES ZONA (ID_ZONA);

ALTER TABLE RUTA_X_ZONA ADD CONSTRAINT FK_RUTA_X_ZONA_RUTA  FOREIGN KEY (ID_RUTA) REFERENCES RUTA (ID_RUTA);

ALTER TABLE RUTA_X_ESTACION ADD CONSTRAINT FK_RUTA_ESTACION__RUTA  FOREIGN KEY (ID_RUTA) REFERENCES RUTA (ID_RUTA);

ALTER TABLE RUTA_X_ESTACION ADD CONSTRAINT FK_RUTA_ESTACION__ESTACIONES  FOREIGN KEY (ID_ESTACION) REFERENCES ESTACIONES (ID_ESTACION);


```
#### HAGO LAS INSERSIONES CORRESPONDIENTES PARA POBLAR LAS TABLAS

```sql
INSERT INTO CONDUCTOR(ID_CONDUCTOR,NOMBRE_CONDUCTOR,APELLIDO_CONDUCTOR)
VALUES
    (1,"Andrés Manuel", "López Obrador"),
    (2,"Nicolás", "Maduro Moros"),
    (3,"Alberto", "Fernández"),
    (4,"Luiz Inácio", "Lula da Silva"),
    (5,"Gabriel", "Boric"),
    (6,"Miguel", "Díaz-Canel"),
    (7,"Daniel", "Ortega"),
    (8,"Gustavo", "Petro Urrego"),
    (9,"Luis", "Arce"),
    (10,"Xiomara", "Castro");
    
INSERT INTO BUS (ID_BUS,PLACA)
VALUES
    (1,"XVH345"),
    (2,"XDL965"),
    (3,"XFG847"),
    (4,"XRJ452"),
    (5,"XDF459"),
    (6,"XET554"),
    (7,"XKL688"),
    (8,"XXL757");
    
    
INSERT INTO ZONA(ID_ZONA, NOMBRE_ZONA) 
VALUES 
(1,"Norte"), 
(2,"Sur"), 
(3,"Oriente"), 
(4,"Occidente"), 
(5,"Floridablanca"), 
(6,"Girón"), 
(7,"Piedecuesta");

INSERT INTO RUTA (ID_RUTA, NOMBRE_RUTA, TIEMPO)
VALUES 
(1,"Universidades", '2:00:00'), 
(2,"Café Madrid", '2:15:00'), 
(3,"Cacique", '1:45:00'), 
(4,"Diamantes", '1:50:00'), 
(5,"Terminal", '2:00:00'), 
(6,"Prado", '1:30:00'), 
(7,"Cabecera", '2:00:00'), 
(8,"Ciudadela", '2:00:00'), 
(9,"Punta Estrella", '2:30:00'), 
(10,"Niza", '2:45:00'), 
(11,"Autopista", '2:15:00'), 
(12,"Lagos", '2:15:00'), 
(13,"Centro Florida", '2:30:00');



INSERT INTO ESTACIONES (ID_ESTACION, NOMBRE_ESTACION)
VALUES 
(1,"Colseguros"), 
(2,"Clínica Chicamocha"), 
(3,"Plaza Guarín"), 
(4,"Mega Mall"), 
(5,"UIS"), 
(6,"UDI"), 
(7,"Santo Tomás"), 
(8,"Boulevard Santander"), 
(9,"Búcaros"), 
(10,"Rosita"), 
(11,"Puerta del Sol"), 
(12,"Cacique"), 
(13,"Plaza Satélite"), 
(14,"La Sirena"), 
(15,"Provenza"), 
(16,"Fontana"), 
(17,"Gibraltar"), 
(18,"Terminal"), 
(19,"Mutis"), 
(20,"Plaza Real");

INSERT INTO RUTA_X_ESTACION (ID_RUTA, ID_ESTACION)
VALUES
(1,1),
(1,2),
(1,3),
(1,4),
(1,5),
(1,6),
(1,7),
(3,8),
(3,9),
(3,10),
(3,11),
(3,12),
(4,13),
(4,14),
(4,15),
(5,16),
(5,17),
(8,18),
(8,19),
(8,20);

INSERT INTO PROGRAMACION (ID_CONDUCTOR,ID_RUTA,ID_ZONA,ID_BUS,DIA)
VALUES
(5,1,1,1,'LUNES'),
(5,1,1,1,'MARTES'),
(5,1,1,3,'MIERCOLES'),
(5,1,1,3,'JUEVES'),
(5,2,1,5,'VIERNES'),
(5,2,1,5,'SABADO'),
(5,2,1,5,'DOMINGO'),
(3,4,4,5,'LUNES'),
(3,4,4,6,'MARTES'),
(3,4,4,1,'MIERCOLES'),
(3,5,4,1,'JUEVES'),
(3,5,4,3,'VIERNES'),
(3,5,4,3,'SABADO'),
(3,5,4,3,'DOMINGO'),
(10,10,5,3,'LUNES'),
(10,10,5,3,'MARTES'),
(10,10,5,5,'MIERCOLES'),
(10,10,5,5,'JUEVES'),
(10,10,5,4,'VIERNES'),
(10,11,5,7,'SABADO'),
(10,11,5,7,'DOMINGO'),
(7,11,5,7,'LUNES'),
(7,11,5,7,'MARTES'),
(6,12,5,7,'MIERCOLES'),
(6,12,5,7,'JUEVES'),
(6,12,5,7,'VIERNES'),
(6,12,5,6,'SABADO'),
(6,12,5,6,'DOMINGO');

```

### Consultas

1. Cantidad de Paradas por Ruta

   ```sql
	 	
   ```
   
   Validacion de la tabla:

   ```bash
   
   
	```
	
2. Nombre de las Paradas de la Ruta Universidades

   ```sql
       SELECT NOMBRE_ESTACION FROM ESTACIONES
       -> JOIN RUTA_X_ESTACION ON ESTACIONES.ID_ESTACION = RUTA_X_ESTACION.ID_ESTACION
       -> JOIN RUTA ON RUTA_X_ESTACION.ID_RUTA = RUTA.ID_RUTA
       -> WHERE NOMBRE_RUTA = 'Universidades';
   
   ```

   Validacion de la tabla:

   ```bash
   +---------------------+
   | NOMBRE_ESTACION     |
   +---------------------+
   | Colseguros          |
   | Clínica Chicamocha  |
   | Plaza Guarín        |
   | Mega Mall           |
   | UIS                 |
   | UDI                 |
   | Santo Tomás         |
   +---------------------+
   ```

3. Nombres de las Rutas No Programadas

   

   ```sql
     	SELECT NOMBRE_RUTA FROM RUTA
       -> LEFT JOIN PROGRAMACION ON RUTA.ID_RUTA = PROGRAMACION.ID_RUTA
       -> WHERE PROGRAMACION.ID_RUTA IS NULL;
   ```

   Validacion de la tabla:

   ```bash
   +----------------+
   | NOMBRE_RUTA    |
   +----------------+
   | Cacique        |
   | Prado          |
   | Cabecera       |
   | Ciudadela      |
   | Punta Estrella |
   | Centro Florida |
   +----------------+
   ```

4. Rutas Programadas sin Conductor Asignado

   ```sql
   SELECT NOMBRE_RUTA FROM RUTA
       -> JOIN PROGRAMACION ON RUTA.ID_RUTA = PROGRAMACION.ID_RUTA
       -> JOIN CONDUCTOR ON PROGRAMACION.ID_CONDUCTOR = CONDUCTOR.ID_CONDUCTOR
       -> WHERE CONDUCTOR.ID_CONDUCTOR IS NULL;
   
   ```

   Resultado:

   ```bash
   Empty set (0,00 sec)
   
   ```

5. Conductores No Asignados a la Programación

   ```sql
   SELECT NOMBRE_CONDUCTOR FROM CONDUCTOR
       -> LEFT JOIN PROGRAMACION ON CONDUCTOR.ID_CONDUCTOR = PROGRAMACION.ID_CONDUCTOR
       -> WHERE PROGRAMACION.ID_CONDUCTOR IS NULL;
   
   ```

   Resultado:

   ```bash
   +------------------+
   | NOMBRE_CONDUCTOR |
   +------------------+
   | Andrés Manuel    |
   | Nicolás          |
   | Luiz Inácio      |
   | Gustavo          |
   | Luis             |
   +------------------+
   ```

6. Buses No asignados a la Programación

   ```sql
   SELECT PLACA FROM BUS
       -> LEFT JOIN PROGRAMACION ON BUS.ID_BUS = PROGRAMACION.ID_BUS
       -> WHERE PROGRAMACION.ID_BUS IS NULL;
   ```

   Resultado:

   ```bash
   +--------+
   | PLACA  |
   +--------+
   | XDL965 |
   | XXL757 |
   +--------+
   ```

7. Zonas NO Programadas

   ```sql
   SELECT NOMBRE_ZONA FROM ZONA
       -> LEFT JOIN PROGRAMACION ON ZONA.ID_ZONA = PROGRAMACION.ID_ZONA
       -> WHERE PROGRAMACION.ID_ZONA IS NULL;
   
   ```

   Resultado:

   ```bash
   +-------------+
   | NOMBRE_ZONA |
   +-------------+
   | Sur         |
   | Oriente     |
   | Girón       |
   | Piedecuesta |
   +-------------+
   ```

8. Programación asignada a cada conductor (Conductor, Ruta y Día)

   ```sql
   
   ```

   Resultado:

   ```bash
   +-----------------+----------------+--------------------------------+
   | NOMBRE_APRENDIZ | NOMBRE_CARRERA | NOMBRE_RUTA                    |
   +-----------------+----------------+--------------------------------+
   | GUSTAVO         | ELECTRONICA    | MICROCONTROLADORES             |
   | PEDRO NELL      | ELECTRONICA    | MICROCONTROLADORES             |
   | JAIRO AUGUSTO   | ELECTRONICA    | ROBOTICA                       |
   | ANTONIO         | SOLDADURA      | SOLDADURA ELECTRICA INDUSTRIAL |
   | DANIEL          | SOLDADURA      | SOLDADURA AUTOGENA INDUSTRIAL  |
   +-----------------+----------------+--------------------------------+
   ```

  

