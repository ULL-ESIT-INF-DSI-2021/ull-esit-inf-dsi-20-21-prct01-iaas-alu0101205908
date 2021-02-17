# PRÁCTICA 1: Configuración de la máquina virtual en el IaaS

En esta primera práctica hemos configurado nuestro entorno de trabajo para la asignatura de Desarrollo de Sistemas Informáticos. En líneas generales, lo que se ha hecho es configurar la máquina virutal (MV) que nos proporciona el IasS (Infraestructura como servicio) de la Universidad de La Laguna, modelando el ecosistema que utilizaremos en esta asignatura.

## Tareas iniciales:

* Para empezar, debemos de tener instalado el software de VPN de la Universidad de La Laguna, para emular que estamos conectados a su red, y así poder acceder a los servicios del IaaS. En nuestro caso, ya tenemos configurada la VPN, dado que ya lo hemos necesitado para otras asignaturas. Una vez activada la VPN de la ULL, nos dirigimos a **[IaaS ULL](https://iaas.ull.es/ovirt-engine/sso/login.html)**, e introducimos nuestras credenciales para poder acceder a nuestro pool de máquinas. 

  * (***En caso de no tener activa la VPN de la ULL, no podremos acceder al link del portal del IaaS***). 

* Una vez dentro del pool, debemos ejecutar la máquina de esta asignatura (**DSI**), y obtendremos nuestra numeración (***16***).

![Numeración][numeracion]

* Y la IP de nuestra máquina (***10.6.130.26***)

![IP][IP]

* A continuación, ya podemos dirigirnos a nuestra máquina Linux (local), y en la consola accederemos por SSH a nuestra MV del IaaS, dado que ya conocemos el nombre de usuario que es ***"usuario"*** y la IP de la máquina. 

   * borja@ubuntu:~$ ssh usuario@10.6.130.26

* Nos saldrá un mensaje al que deberemos responder con ***"yes"***, y nos pedirá una contraseña, que será ***"usuario"***.
  
  * Una vez aceptado el mensaje, deberemos cambiar la contraseña, introduciendo primeramente la contraseña "usuario", y posteriormente la nueva (repitiéndola dos veces).
  

* En caso de no tener el software de VPN instalado, se recomienda leer la siguiente documentación: **[VPN ULL](https://www.ull.es/servicios/stic/2020/12/01/servicio-de-vpn-de-la-ull/)**

## Generación de claves máquina virtual:

* En la MV, vamos a generar una nueva pareja de clave pública-privada, dado que en la MV no tenemos niguna. Para ello, introducimos el siguiente comando:

  * usuario@ubuntu:~$ ssh-keygen

* Para ver la clave publica que hemos generado hacemos:

  * usuario@ubuntu:~$ cat .ssh/id_rsa.pub 

* Ahora deberarmos copiar dicha clave y la tendremos que poner junto a nuestras claves públicas en GitHub. Para ello, deberemos dirigirnos a los ajustes de nuestra cuenta de GitHub y añadir la clave pública:

* Vamos a ajustes:
 
![Ajustes][Settings1]

* Añadimos la clave generada:

![New SSH][Settings2]

![New SSH key][Settings3]

## Instalación de Git en la máquina virtual:

* A continuación, vamos a instalar Git, el sistema de control de versiones que utilizaremos. En nuestro caso, ya viene instalado. Para proceder a su instalación debemos introducir la siguiente sentencia:

  * usuario@ubuntu:~$ sudo apt install git

* Seguidamente, procedemos a configurarlo, que no es otra cosa que poner nuestro nombre y nuestro correo en la configuración global de git de nuestra MV:

  * usuario@ubuntu:~$ git config --global user.name "Borja Guanche"

  * usuario@ubuntu:~$ git config --global user.email alu0101205908@ull.edu.es

    * ***NOTA:*** Si ejectamos el siguiente comando, podremos ver la configuración del git:
    
      * usuario@ubuntu:~$ git config --list
      * ![Git config][gitConfig]


[Numeracion]: images/numeracion.JPG "Numeración"
[IP]: images/IP.JPG "IP"
[UsuarioIP]: images/usuariosIP.JPG "Usuario@IP"
[Settings1]: images/settings1.JPG "Ajustes"
[Settings2]: images/settings2.jpg "New SSH"
[Settings3]: images/settings3.jpg "New SSH key"
[gitConfig]: images/settings3.jpg "Git config"
