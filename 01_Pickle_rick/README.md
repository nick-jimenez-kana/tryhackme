



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

Al parecer el Command Panel esta bloqueado algunas comandos
![alt text](image-13.png)

> el command panel no esta bloqueando el coamndo `grep` asi que haremos una busqueda recursiva 
![alt text](image-14.png)

veamos su codigo del resulado de la busqueda

> enontramos el usuario ``R1ckRul3s`` y el password ``Wubbalubbadubdub``
![alt text](image-15.png)

> tambien vemos un script donde esta la lista negra de comandos del Command Panel
![alt text](image-16.png)

> mandamos un `ls` y nos damos con el grata sopresa que tenemos algunos archivos que ya vimos pero no todos  
![alt text](image-12.png)

> vemos que en el archivo `Sup3rS3cretPickl3Ingred.txt` encontramos `mr. meeseek hair` al parecer peude ser la priemra receta
![alt text](image-17.png)

> nos pide que busquemos en otro ficheros del sistemas
![alt text](image-18.png)

> revisaremos el fichero raiz
![alt text](image-20.png)

> nos da los suarios `rick` y `ubuntu`
![alt text](image-21.png)

> al revisar el usuario `rick` encontramos al parecer nuestra segunda respuesta y la revisaremos a ver que sale y encontramos la 2do ingredient: `1 jerry tear`
![alt text](image-22.png)
![alt text](image-23.png)

> haremos un reverse shell con bash primero buscaremos el script en de reverse sheel con bash y cambiamos los atributos y hacemos un `listener` en el port `1234` y ejecutamos el el scrip y estamos dentro 
![alt text](image-24.png)

> entramos a `/root` y listamos archivos y encontramos 3rd ingredients: `fleeb juice`
![alt text](image-25.png)

















# Pickle Rick

<p align="left">
  <a href='report-picklerick.pdf.pdf'>
    <img width="50%" src="assets/report-pickle_rick.jpg" alt="Pickle Rick Report" />
  </a>
</p>

Este documento detalla todo el proceso de enumeración, análisis, explotación y escalamiento realizado sobre la máquina **10.201.17.154**, acompañado de todas las evidencias y capturas usadas durante el pentest.

---

## 📡 1. Verificación de conectividad — Ping ICMP

Se realizó un ping de **solo 2 paquetes ICMP** para validar la conectividad entre la máquina atacante y la víctima.

![alt text](assets/image.png)

---

## 🔍 2. Escaneo Nmap

Se ejecutó un escaneo con **Nmap** para identificar los puertos abiertos y generar el archivo:

10.201.17.154_nmap.txt


![alt text](assets/image-1.png)

---

## 🌐 3. Enumeración con Nikto y Gobuster

### 🔸 Nikto
Nikto reveló el endpoint **/login.php**.

![alt text](assets/image-4.png)

### 🔸 Gobuster
Gobuster enumeró múltiples directorios con distintos códigos de estado y tamaños.

![alt text](assets/image-5.png)

---

## 🕸️ 4. Análisis de la aplicación web (port 80)

### 🏠 Página principal
Home de `http://10.201.17.154/`

![alt text](assets/image-2.png)

### 🔎 Código fuente
En el código fuente se identificó un comentario con:

- **Username:** `R1ckRul3s`

![alt text](assets/image-3.png)

---

## 📂 5. Revisión de rutas encontradas

### 🔸 /login.php y /portal
Ambas rutas llevan al mismo formulario login.  
Se encontró un usuario: **R1ckRul3s**  
Y probamos como contraseña: **Wubbalubbadubdub** (encontrada en `/robots.txt`)

![alt text](assets/image-6.png)

---

### 🔸 /assets
Esta ruta solo contiene archivos de Bootstrap e imágenes.

![alt text](assets/image-7.png)

---

### 🔸 /robots.txt
Revela una cadena sospechosa que se usará como contraseña.

![alt text](assets/image-8.png)

---

## 🔐 6. Acceso a la web

Se logró ingresar con:

- **Usuario:** `R1ckRul3s`
- **Contraseña:** `Wubbalubbadubdub`

![alt text](assets/image-9.png)

---

## 🧪 7. Inyección de comandos (Command Panel)

Dentro de la aplicación se encontró un panel llamado **Command Panel**.

### 🔸 Probando comando `pwd`
Confirmamos la ruta del sistema:

/var/www/html


![alt text](assets/image-10.png)

---

### 🔸 Comandos bloqueados
El panel bloquea varios comandos.

![alt text](assets/image-13.png)

---

### 🔸 El comando `grep` NO está bloqueado  
Se ejecutó una búsqueda recursiva:

![alt text](assets/image-14.png)

Resultado del código:

![alt text](assets/image-15.png)

Aquí encontramos nuevamente:

- **Usuario:** `R1ckRul3s`
- **Password:** `Wubbalubbadubdub`

---

### 🔸 Lista negra de comandos
Se encuentra un script donde se define el **blacklist** del Command Panel.

![alt text](assets/image-16.png)

---

## 📄 8. Exploración de archivos del sistema

Se listan archivos:

![alt text](assets/image-12.png)

---

### 🔸 Ingrediente 1
Archivo: `Sup3rS3cretPickl3Ingred.txt`  
Contenido: **mr. meeseek hair**

![alt text](assets/image-17.png)

---

### 🔸 Revisión del directorio raíz

![alt text](assets/image-18.png)

Usuarios encontrados:

- rick  
- ubuntu

![alt text](assets/image-21.png)

---

### 🔸 Ingrediente 2 (usuario rick)

![alt text](assets/image-22.png)

Dentro encontramos:

- **2nd ingredient:** `1 jerry tear`

![alt text](assets/image-23.png)

---

## 🌀 9. Reverse Shell — Escalada a usuario / root

Se preparó un reverse shell con **bash**, se creó el script, se cambió permisos y se levantó un listener en el puerto **1234**.

![alt text](assets/image-24.png)

Una vez ejecutado el script:  
**Acceso concedido dentro del sistema.**

---

## 👑 10. Escalada final — Usuario root

Se ingresó al directorio `/root`:

![alt text](assets/image-25.png)

### 🔸 Ingrediente 3:
- **fleeb juice**

---

# 🏁 Resultado Final

Ingredientes encontrados:

1. **mr. meeseek hair**  
2. **1 jerry tear**  
3. **fleeb juice**

Pentest completado con:

- Enumeración completa  
- Explotación vía Command Injection  
- Reverse Shell  
- Escalada de privilegios  
- Captura de todos los flags / ingredientes  

---

## ✨ Autor

Pentesting realizado por **Nick Jimenez**  
📌 Para investigación, educación y práctica de hacking ético.

