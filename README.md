# create database Almacen;
use Almacen;

create table Almacen (nro int auto_increment primary key, nombre varchar(20), responsable varchar(20)); 			
create table Articulo (cod_art int auto_increment primary key, descripción varchar(20), precio double(5,5)); 		
create table Material (cod_mat int auto_increment primary key, descripción varchar(20));
 create table Ciudad(cod_ciu int auto_increment primary key, nombre varchar(20));

create table Proveedor (
cod_prov int auto_increment primary key, nombre varchar(20), domicilio varchar(20), cod_ciu int , fecha_alta date,
foreign key(cod_ciu) references  Ciudad(cod_ciu));
	

create table Contiene (nro int , cod_art int ,
foreign key (nro) references Almacen(nro),
foreign key (cod_art) references Articulo (cod_art) 
); 			

create table Compuesto_por (cod_art int, cod_mat int,
foreign key ( cod_art) references Articulo (cod_art),
foreign key (cod_mat) references Material(cod_mat)
)
;
create table Provisto_por (cod_mat int, cod_prov int 
,foreign key (cod_mat) references Material (cod_mat ),
foreign key (cod_prov) references Proveedor(cod_prov)
 ) ;
 
 /*1 Listar los números de artículos cuyo precio se encuentre entre $100 y $1000 y su descripción comience con la letra A. */

select cod_art
from Articulo 
where precio > 100 or precio <1000  and
descripcion like "A%";

 
 /*
2.	Listar todos los datos de todos los proveedores.
3.	Listar la descripción de los materiales de código 1, 3, 6, 9 y 18.
4.	Listar código y nombre de proveedores de la calle Suipacha, que hayan sido dados de alta en el año 2001.
5.	Listar nombre de todos los proveedores y de su ciudad.
6.	Listar los nombres de los proveedores de la ciudad de La Plata.
7.	Listar los números de almacenes que almacenan el artículo de descripción A.
8.	Listar los materiales (código y descripción) provistos por proveedores de la ciudad de Rosario.
9.	Listar los nombres de los proveedores que proveen materiales para artículos ubicados en almacenes que Martín Gómez tiene a su cargo.
10.	Mover los artículos almacenados en el almacén de número 10 al de número 20.
11.	Eliminar a los proveedores que contengan la palabra ABC en su nombre
12.	Indicar la cantidad de proveedores que comienzan con la letra F.
13.	Listar el promedio de precios de los artículos por cada almacén (nombre)
14.	Listar la descripción de artículos compuestos por al menos 2 materiales.
15.	Listar cantidad de materiales que provee cada proveedor (código, nombre y domicilio)
16.	Cuál es el precio máximo de los artículos que proveen los proveedores de la ciudad de Zárate.
17.	Listar los nombres de aquellos proveedores que no proveen ningún material.
18.	Listar los códigos de los materiales que provea el proveedor 10 y no los provea el proveedor 15.
19.	Listar número y nombre de almacenes que contienen los artículos de descripción A y los de descripción B (ambos).
20.	Listar la descripción de artículos compuestos por todos los materiales.
21.	Hallar los códigos y nombres de los proveedores que proveen al menos un material que se usa en algún artículo cuyo precio es mayor a $100.
22.	Listar la descripción de los artículos de mayor precio.
23.	Listar los nombres de proveedores de Capital Federal que sean únicos proveedores de algún material.
24.	Listar los nombres de almacenes que almacenan la mayor cantidad de artículos.
25.	Listar la ciudades donde existan proveedores que proveen todos los materiales.
26.	Listar los números de almacenes que tienen todos los artículos que incluyen el material con código 123.


*/
 





























-------------------------------------------------------------------------------------------------------------------------------------------------------------------











PELICULA  

 CREATE TABLE proveedor(
  CUIT BIGINT PRIMARY KEY,
  nombre VARCHAR(30) NOT NULL,
  domicilio VARCHAR(40),
  telefono BIGINT NOT NULL,
  MAIL VARCHAR(50)
);
CREATE TABLE localidad(
  id_localidad INT PRIMARY KEY AUTO_INCREMENT,
  Cod_post SMALLINT NOT NULL,
  Descripcion VARCHAR(40)
  );
  CREATE TABLE GeneroPelicula(
  id_Genero int PRIMARY KEY AUTO_INCREMENT,
  Abrev VARCHAR(10),
  Descripcion VARCHAR(20) 
  );
  CREATE TABLE pelicula (
    cod_pel VARCHAR(8) PRIMARY KEY,
    titulo VARCHAR(40) NOT NULL,
    id_genero INT,
    CUIT_prov BIGINT,
FOREIGN KEY(CUIT_prov) REFERENCES proveedor(CUIT),
FOREIGN KEY(id_genero) REFERENCES GeneroPelicula(id_Genero) 
  );
 
 CREATE TABLE CLIENTE (
 id_Cliente INT PRIMARY KEY,
 Tipo_Doc VARCHAR(5),
 Nro_Doc BIGINT NOT NULL,
 Nombre VARCHAR(30) NOT NULL, 
 Telefono BIGINT,
 Domicilio_Calle VARCHAR(20),
 Domicilio_Nro SMALLINT,
 Domicilio_Piso TINYINT,  
 Domicilio_Depto VARCHAR(5),
 id_Localidad INT,
 F_Nacimiento date,
 id_Cliente_Titular INT,
 FOREIGN KEY (id_Localidad) REFERENCES LOCALIDAD(id_localidad),
 FOREIGN KEY (id_Cliente_Titular) REFERENCES CLIENTE(id_Cliente)  
 ); 
 CREATE TABLE Alquiler(
 cod_pel VARCHAR(8),
 idCliente INT,
 fecha DATE,
 Fecha_Dev DATE,
 importe SMALLINT,
 PRIMARY KEY (cod_pel,idCliente),
 FOREIGN KEY (cod_pel) REFERENCES pelicula(cod_pel),
 FOREIGN KEY (idCliente) REFERENCES CLIENTE(id_Cliente)
 );
 
 INSERT INTO proveedor(CUIT,nombre,domicilio,telefono,mail) 
 VALUES (23252221117,"Distribuidora1","arieta1555",54662200,"hola@hotmail.com"),
 (45254544571,"Juan Perez",NULL,23523256,NULL),
 (3365465410,"Andres Gonzales",NULL,33665544,"andres@gmail.com");
 
 INSERT INTO Localidad(id_localidad,Cod_post,Descripcion)VALUES
(1,1753,"VILLA LUZURIAGA"),
(2,1752,"LOMAS DEL MIRADOR"),
(3,1754,"SAN JUSTO"),
(4,1778,"CIUDAD EVITA"),
(5,1785,"ALDO BONZI"),
(6,1768,"CIUDAD MADERO"),
(7,1704,"RAMOS MEJIA");
 
 INSERT INTO GeneroPelicula(id_Genero,Abrev,Descripcion) VALUES
(1,"COM","COMEDIA"),
(2,"COMR","COMEDIA ROMANTICA"),
(3,"ACC","ACCION"),
(4,"AVE","AVENTURA"),
(5,"DRA","DRAMA"),
(6,"TER","TERROR"),
(7,"MUS","MUSICAL"),
(8,"CFIC","CIENCIA FICCION"),
(9,"BEL","BELICA"),
(10,"INF","INFANTIL"),
(11,"SUSP","SUSPENSO");
   
INSERT INTO pelicula(cod_pel,titulo,id_genero,CUIT_prov)VALUES
("A1","EL PADRINO",5,23252221117),
("A2","CINEMA PARADISO",5,23252221117),
("A3","FORREST GUMP",5,3365465410),
("A4","EL CLUB DE LA PELEA",5,3365465410),
("A5","MAGO DE OZ",7,45254544571),
("A6","CANTANDO BAJO LA LLUVIA",7,45254544571),
("A7","DIRTY DANCING",7,45254544571),
("A8","MOULING ROUGE",7,45254544571),
("A9","TOY STORY 1",10,3365465410),
("A10","RATATUILLE",10,3365465410),
("A11","UP",10,23252221117),
("A12","LA MASCARA",1,23252221117),
("A13","LOCO POR MARY",1,3365465410),
("A14","SCARY MOVIE",1,3365465410),
("A15","2001:ODISEA DEL ESPACIO",8,23252221117),
("A16","E.T EL EXTRATERRESTE",8,23252221117),
("A17","MATRIX",8,23252221117),
("A18","INDIANA JONE:EN BUSCA DEL ARCA PERDIDA",4,3365465410),
("A19","CUENTA CONMIGO",4,3365465410),
("A20","NAUFRAGO",4,3365465410),
("A21","SENDEROS DE GLORIA",9,23252221117),
("A22","LA VIDA ES BELLA",9,23252221117);
    
INSERT INTO CLIENTE (id_Cliente,Tipo_Doc,Nro_Doc,Nombre,Telefono,Domicilio_Calle,Domicilio_Nro,Domicilio_Piso,Domicilio_Depto,id_Localidad,F_Nacimiento,id_Cliente_Titular) VALUES
(1,"DNI",1111,"JUAN",111223344,"ARIETA",1522,1,"A",1,1/5/1995,NULL),
(2,"DNI",2222,"ANDRES",111234556,"ARIETA",3522,NULL,NULL,3,18/12/1985,1),
(3,"DNI",3333,"MARCELA",111223355,"AVENIDA DE MAYO",522,4,"C",7,3/6/1999,1),
(4,"DNI",4444,"JOSE",111234577,"BOLIVAR",650,6,"41",7,4/2/1977,NULL),
(5,"DNI",5555,"DIEGO",111223399,"ROSALES",322,1,"A",7,8/9/1979,NULL),
(6,"DNI",6666,"MAURO",NULL,"REPUBLICA DE CHILE",3052,NULL,NULL,3,5/11/1996,NULL), 
(7,"DNI",7777,"KARINA",NULL,"JUJUY",3501,NULL,NULL,3,10/8/1999,6),
(8,"DNI",8888,"VALERIA",111234556,"ALSINA",155,3,"C",7,5/4/1987,NULL),
(9,"DNI",9999,"LARA",111234556,"REPUBLICA DE CHILE",155,NULL,NULL,1,10/9/1999,NULL);
 
 INSERT INTO Alquiler(cod_pel,idCliente,fecha,Fecha_Dev,importe) VALUES
("A5",2,20210502,20210503,150),
("A6",2,20210716,20210717,300),
("A12",3,20210929,20211002,300),
("A17",4,20210527,20210528,150),
("A20",3,20210925,20210926,150),
("A17",3,20210925,20210926,150),
("A20",7,20210717,20210718,150),
("A12",8,20210909,20210911,250),
("A19",3,20210626,20210628,250),
("A7",7,20210611,20210614,300),
("A8",2,20210909,20210910,150),
("A20",2,20210621,20210622,150),
("A12",7,20210610,20210611,150),
("A7",8,20210829,20210830,150),
("A6",9,20210717,20210718,150),
("A5",7,20210819,20210821,250);







