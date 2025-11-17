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
