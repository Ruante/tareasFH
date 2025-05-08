# Configuración de Red

## Descripción de la tarea
Vamos a llevar a cabo la configuración de una pequeña red con dos máquinas.

## Pasos de la tarea

1. **Crea dos máquinas virtuales** (mediante clonación enlazada y reinicializando las direcciones MAC). Al hacerlo, los equipos serán visibles a través del interfaz de red `enp0s8` (segundo adaptador de red virtual que implementa en VirtualBox una conexión de red interna a la red “intnet”). 

    - Para generar una nueva MAC en el proceso de instalación seleccionamos lo siguiente (Hacemos lo mismo en la B):

        ![Captura](Screenshots/Captura%20de%20pantalla%202025-05-08%20105206.png)

     - Conectamos los dos adaptadores, el primero en NAT y el segundo en Interna, además podemos generar una nueva MAC dándole al icono de actualizar.

        ![Captura](Screenshots/Captura%20de%20pantalla%202025-05-08%20105433.png)

        ![Captura](Screenshots/Captura%20de%20pantalla%202025-05-08%20105554.png)

2. **Configura las interfaces de red `enp0s8`** de ambos equipos de forma que estén en la red IP `192.168.100.0/24` de forma no permanente. Usa la segunda y tercera IP de host disponible de esta red respectivamente. En esta la red interna “intnet” VirtualBox se considerará que no existe DHCP y se usará, por tanto, una configuración estática. 

    - Para comenzar usaremos un `sudo su` para entrar como root. Luego usaremos un `ip` para añadir una IP no persistente a la interfaz `enp0s8` la cual se perdería si se llega a reiniciar el equipo. Para comprobar la IP hacemos un `ip a`.

   - **Máquina A:**

        ![Captura](Screenshots/Captura%20de%20pantalla%202025-05-08%20110451.png)

   - **Máquina B:**

        ![Captura](Screenshots/Captura%20de%20pantalla%202025-05-08%20111257.png)

3. **Comprueba que los equipos se pueden ver usando ping.**
   - De Máquina A a Máquina B:

        ![Captura](Screenshots/Captura%20de%20pantalla%202025-05-08%20111949.png)

   - De Máquina B a Máquina A:

        ![Captura](Screenshots/Captura%20de%20pantalla%202025-05-08%20111828.png)

4. **Haz que la configuración de ambas redes sea persistente.** Máquina A mediante Netplan y Máquina B mediante NetworkManager. 

   - En la Máquina A lo haremos en Netplan, para ello iremos a `nano /etc/netplan/01-network-manager-all.yaml` y pondremos la siguiente información:

        ![Captura](Screenshots/Captura%20de%20pantalla%202025-05-08%20112905.png)

   - En la Máquina B lo haremos mediante NetworkManager. Para ello vamos a Configuración -> Red -> Enp0s8 -> IPV4 y lo configuraremos de tal manera:

        ![Captura](Screenshots/Captura%20de%20pantalla%202025-05-08%20120649.png)
