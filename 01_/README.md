 $TARGET_IP= 10.201.17.154

 ✅ crear un directorio  de la habitacion
 ✅ crea un directoria por fase de ataqeu ping, nmap, nikto, gobuster
 ✅ hacer un ping con la maquina atacante.

Se esta realizando un ping de solo 2 paquetes ICMP para ver la conectividad entra la maquina atacante con la aquina victima que tine una IP 10.201.17.154.

![alt text](image.png)

✅ hacer un escaneo con nmap

Se realiza un escaneo con nmap para ver los todos los puertos abiertos y nos de un reporte en un documento 10.201.17.154_nmap.txt

![alt text](image-1.png)

✅ hacer una enumeracion con nikto
✅ hacer otra enumaeracion gobuster
✅ mientras se naaliza la aplicacion web y codigo por port 80

Home de pagina web de http://10.201.17.154/ 
![alt text](image-2.png)

En el codigo fuente del la pagina http://10.201.17.154/  se encontro una cpmentario con un Username: R1ckRul3s
![alt text](image-3.png)

✅ Ver y analizar los resultados que da nikto y gobuster
 Nikto
 El esceno de nikto nos da como resultado que tenemos un /login.php habilitado.
 ![alt text](image-4.png)
 
 Gobuster
 El escaneo de gobuster nos da unos enumera unos directorios algunos con sus status y el tamaño del directorio.
 ![alt text](image-5.png)


✅ verificas paginas entradas 
 /login.php y /portal llevan al mismo fichero donde encontramos un login pero nos pide username y password pero conseguimos un Username: R1ckRul3s en un comentario probaremos con esto con Wubbalubbadubdub en el fichero /robots.txt.
 ![alt text](image-6.png)

 /asset encontramos puro archivos de codigo boostrap con iamgenes 
  ![alt text](image-7.png)

 /robots.txt se encontro un cadena de text lo cual se probara para la contraseña de /login 
 ![alt text](image-8.png)

 Se logro ingreasar con las credenciales Username: R1ckRul3s Password: Wubbalubbadubdub
 ![alt text](image-9.png)


10. hacer inyeccion de comandos 

Se encontro varias pestañas dentro de la aplicacion web pero solo nos permiten ingresar a Command Panel donde ingremaos un pwd y nos da como la ruta de la ubicacion del fichero /var/www/html

![alt text](image-10.png)

mandamos un ls y nos damos con el grata sopresa que tenemos algunos archivos que ya vimos pero no todos  
![alt text](image-12.png)

Al parecer el Command Panel esta bloqueado algunas comandos
![alt text](image-13.png)

11. hace shhel inverso con netcat y python3

12. utiliza el tools de mi pobre hombre 


Questions

1. ¿Cuál es el primer ingrediente que necesita Rick?
´´´

´´´
2. ¿Cuál es el segundo ingrediente de la poción de Rick?


3. ¿Cuál es el último y definitivo ingrediente?










Recomendations 

- Va haceindo notas mientras ataca
- Definir o dar conceptos a un libro de tools
- necesitamos conocimiento de rogramcion para entender que hace

Vulns

Command Injection(Injeccion de comandos): es una vulnerabilidad grave, la cual el atacante inserta comandos dentro de una cadena que va a ejecutar el sistema operativo.


Reverse Shell (Shell Inverso): es cuando el atacante logra terner acceso a una shell remta de la maquina de la victima.

Tools 

Netcat (nc - navaja suiza de la red): tools que permite abrir conexiones TCP/UDP, montar un listener (escuchar puertos), enviar/recibir datos, hacer banner grabbing (cabecera de un servicio)

Rockyou: es una diccionario de contraseñas usualmente se usa para wordlist en ataques de fuerza bruta y password craking para pruebas defensivas y crear reglas de hadenign

