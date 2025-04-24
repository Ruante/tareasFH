# Tarea SSH y SCP

## 1. Conexión en la misma red usando SSH

Se configuran los puertos de ambas máquinas y sus redes:
- **Máquina A**: Puerto 2222
  
	![Captura](Screenshots/Captura_de_pantalla_2025-04-24%20173709.png)

	![Captura](Screenshots/Captura%20de%20pantalla%202025-04-24%20173724.png)

- **Máquina B**: Puerto 2223

	![Captura](Screenshots/Captura%20de%20pantalla%202025-04-24%20173733.png)

	![Captura](Screenshots/Captura%20de%20pantalla%202025-04-24%20173743.png)
	
	**Configuración de red:**
	1. Ir a **Configuración → Red**.
	2. En la tarjeta de red `enp0s8`, hacer clic en la ruedita de configuración.
	3. Configurar los parámetros como en la imagen proporcionada.(La puerta de enlace no es necesaria).
   
	- Máquina Cliente o A:

	![Captura](Screenshots/Captura%20de%20pantalla%202025-04-24%20173819.png)

	- Máquina Servidor o B:
  
	![Captura](Screenshots/Captura%20de%20pantalla%202025-04-24%20173826.png)

	<br><br>
	
## 2. Creación de usuarios

- En la **Máquina A** se creó el usuario: `alex`

	```bash
	sudo adduser alex
	```
	
	![Captura](Screenshots/Captura%20de%20pantalla%202025-04-24%20173806.png)

- En la **Máquina B** se creó el usuario: `brais`
  
	```bash
	sudo adduser brais
	```

	![Captura](Screenshots/Captura%20de%20pantalla%202025-04-24%20173813.png)

	<br><br>
## 4. Conexión desde A hacia B

Se realiza con el comando:

```bash
ssh brais@192.168.100.20
```

![Captura](Screenshots/Captura%20de%20pantalla%202025-04-24%20173834.png)

**Explicación del comando:**
- `ssh`: comando para conectarse por SSH.
- `brais`: nombre de usuario en la máquina B.
- `192.168.100.20`: dirección IP del servidor (máquina B).

 Al conectarse por primera vez, el cliente guarda la clave pública del servidor en la carpeta **~/.ssh/known_hosts**.
 <br><br>

## 5. Envío de archivos desde cliente (máquina A) al servidor (máquina B)

- En el cliente hacemos lo siguiente:
```bash
mkdir /tmp/prueba
echo "contenido de prueba" > /tmp/prueba/prueba.txt
scp -P 2223 -r /tmp/prueba brais@192.168.100.20:/tmp/
```

![Captura](Screenshots/Captura%20de%20pantalla%202025-04-24%20173841.png)

![Captura](Screenshots/Captura%20de%20pantalla%202025-04-24%20173847.png)

El scp sirve para mandar archivos como el anterior al servidor por ejmplo.
<br><br>

## 6. Envío de archivos desde el servidor al cliente

- En el servidor hacemos lo siguiente:
```bash
mkdir /tmp/prueba2
echo "contenido prueba2" > /tmp/prueba2/prueba2.txt
scp -P 2222 -r brais@192.168.100.20:/tmp/prueba2 /tmp/
```

![Captura](Screenshots/Captura%20de%20pantalla%202025-04-24%20173855.png)

![Captura](Screenshots/Captura%20de%20pantalla%202025-04-24%20173902.png)

<br><br>

## 7. Transferencia a ordenador anfitrión

Para transmitir los directorios **prueba** y **prueba2** al equipo anfitrion o al real usamos los siguientes dos comandos:

```bash
scp -r -P 2222 alex@localhost:/tmp/prueba C:\Users\ASIR127\Desktop
scp -r -P 2223 brais@localhost:/tmp/prueba2 C:\Users\ASIR127\Desktop
```

![Captura](Screenshots/Captura%20de%20pantalla%202025-04-24%20173912.png)

<br><br>

## 8. Crear y transferir "prueba3" con 200 archivos

En el servidor o con ssh desde A usamos los siguientes comandos:

```bash
mkdir /tmp/prueba3 && for i in $(seq 1 200); do touch /tmp/prueba3/archivo$i.txt; done
```

![Captura](Screenshots/Captura%20de%20pantalla%202025-04-24%20173921.png)

Transferirmos al escritorio:

```bash
scp -r -P 2223 brais@localhost:/tmp/prueba3 C:\Users\ASIR127\Desktop
```

![Captura](Screenshots/Captura%20de%20pantalla%202025-04-24%20173927.png)

<br><br>

## 9. Conexión por clave SSH

Ceamos una llave de la siguiente manera con el passphrase **servidorssh**:

```bash
ssh-keygen -t rsa -b 4096
```

![Captura](Screenshots/Captura%20de%20pantalla%202025-04-24%20173936.png)

Se la compartimos al servidor:

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub brais@192.168.100.20
```

![Captura](Screenshots/Captura%20de%20pantalla%202025-04-24%20173944.png)

Por ultimo utilizamos la clave creada para acceder por ssh:

```bash
ssh -i ~/.ssh/id_rsa brais@192.168.100.20
```

![Captura](Screenshots/Captura%20de%20pantalla%202025-04-24%20173951.png)

<br>

<div style="display: flex; justify-content: space-between;">
  <span>David Rodríguez López</span>
  <span>1ºASIR</span>
</div>