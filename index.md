# PRÁCTICA 1: Configuración de la máquina virtual en el IaaS

En esta primera práctica hemos configurado nuestro entorno de trabajo para la asignatura de Desarrollo de Sistemas Informáticos. En líneas generales, lo que se ha hecho es configurar la **[máquina virtual](https://es.wikipedia.org/wiki/M%C3%A1quina_virtual)** (MV) que nos proporciona el **[IasS](https://es.wikipedia.org/wiki/Infraestructura_como_servicio_(IaaS))** (Infraestructura como servicio) de la Universidad de La Laguna, modelando el ecosistema que utilizaremos en esta asignatura.

Para acceder a la GitHub page: **[AQUÍ](https://ull-esit-inf-dsi-2021.github.io/ull-esit-inf-dsi-20-21-prct01-iaas-alu0101205908/)** 

## Tareas iniciales:

* Para empezar, debemos de tener instalado el software de **[VPN](https://es.wikipedia.org/wiki/Red_privada_virtual)** de la Universidad de La Laguna, para emular que estamos conectados a su red, y así poder acceder a los servicios del IaaS. En nuestro caso, ya tenemos configurada la VPN, dado que ya lo hemos necesitado para otras asignaturas. Una vez activada la VPN de la ULL, nos dirigimos a **[IaaS ULL](https://iaas.ull.es/ovirt-engine/sso/login.html)**, e introducimos nuestras credenciales para poder acceder a nuestro pool de máquinas. 

  * (***En caso de no tener activa la VPN de la ULL, no podremos acceder al link del portal del IaaS***). 

* Una vez dentro del pool, debemos ejecutar la máquina de esta asignatura (**DSI**), y obtendremos nuestra numeración (***16***).

![Numeración][numeracion]

* Y la IP de nuestra máquina (***10.6.130.26***)

![IP][IP]

* A continuación, ya podemos dirigirnos a nuestra máquina Linux (local), y en la consola accederemos por **[SSH](https://es.wikipedia.org/wiki/Secure_Shell)** a nuestra MV del IaaS, dado que ya conocemos el nombre de usuario que es ***"usuario"*** y la IP de la máquina. 

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

* A continuación, vamos a instalar **[Git](https://es.wikipedia.org/wiki/Git)**, el sistema de control de versiones que utilizaremos. En nuestro caso, ya viene instalado. Para proceder a su instalación debemos introducir la siguiente sentencia:

  * usuario@ubuntu:~$ sudo apt install git

* Seguidamente, procedemos a configurarlo, que no es otra cosa que poner nuestro nombre y nuestro correo en la configuración global de git de nuestra MV:

  * usuario@ubuntu:~$ git config --global user.name "Borja Guanche"

  * usuario@ubuntu:~$ git config --global user.email alu0101205908@ull.edu.es

    * ***NOTA:*** Si ejecutamos el siguiente comando, podremos ver la configuración del git:
    
      * usuario@ubuntu:~$ git config --list
       
      ![Git config][gitConfig]
      
## Cambio del prompt en la máquina virtual:

* Vamos a cambiar el **[prompt](https://es.wikipedia.org/wiki/Prompt)** que tenemos en la terminal de nuestra MV, para que cuando estemos dentro de un repositorio, aparezca la rama actual en el prompt. Esto nos va a ayudar a evitar hacer un git branch para ver la rama activa actualmente. Para hacer el cambio, primero se deberá acceder al siguiente enlace **[GIT PROMPT](https://github.com/git/git/blob/master/contrib/completion/git-prompt.sh)**.

   1. Copiaremos todo el fichero del enlace anterior, y lo pegaremos en un nuevo fichero en nuestra MV que denominaremos ***"git-prompt.sh"***. 
   2. Ejecutaremos el siguiente comando: usuario@ubuntu:~$ mv git-prompt.sh .git-prompt.sh
   3. Abrimos el fichero ***.bashrc***, y en las últimas líneas agregamos las siguiente líneas:
   
     source ~/.git-prompt.sh
     
           PS1='\[\033]0;\u@\h:\w\007\]\[\033[0;34m\][\[\033[0;31m\]\w\[\033[0;32m\]($(git branch 2>/dev/null | sed -n "s/\* \(.*\)/\1/p"))\[\033[0;34m\]]$'
 
    4. Reiniciamos la terminal: usuario@ubuntu:~$ exec bash -l
   
* Como veremos, el formato ha cambiado:

![Prompt cambiado][cambioPrompt]

* Para comprobar que realiza su función, vamos a clonar un repositorio de GitHub, y veremos si cumple su función:

![Prompt rama][promptRama]

## Instalación de node, nvm y npm en la máquina virtual:

* Finalmente, procederemos a la instalación del gestor de versiones de **[node.js](https://es.wikipedia.org/wiki/Node.js)** ***nvm (node version manager)***, el propio ***node.js*** y el gestor de paquetes de node ***npm (node package manager)*** en nuestra MV. Son herramientas que utilizaremos en la asignatura para gestionar el entorno node.js y trabajar con código JavaScript o TypeScript. Lo haremos de la siguiente manera:

   1. Ejecutamos el siguiente comando para instalar ***nvm***: 
   
          $wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash
   2. Reiniciamos la terminal: $exec bash -l
   3. Comprobamos la versión de ***nvm***: $nvm --version
   
   ![Version nvm][nvm]
   
   4. Ejecutamos el siguiente comando para instalar ***node*** y ***npm***: $nvm install node

   ![Version de node y npm][node&npm]
   
* Si queremos instalar un versión determinada de node, o queremos cambiar la versión por otra que ya hemos instalado, solamente deberemos de hacer:

  * $nvm install 12.0.0
  * $nvm use v15.8.0 

## Opcional:

* De manera opcional, vamos a cambiar ciertos parámetros para por ejemplo, no tener que recordar la dirección IP de la MV.

* En primer lugar, vamos a cambiar el nombre de la máquina, de ***ubuntu*** --> ***iaas-dsi16***, que es el número que se nos asignó. Para ello haremos:

  * Ejecutamos el comando: sudo vi /etc/hostname
  * Cambiamos el nombre ***ubuntu*** por ***iaas-dsi16***

  ![cat /etc/hostname en MV][hostName]

* En segundo lugar, vamos a cambiar el nombre asignado a la dirección 127.0.1.1, de ***ubuntu*** --> ***iaas-dsi16***. Para ello haremos:

  * Ejecutamos el comando: sudo vi /etc/hosts
  * Cambiamos el nombre ***ubuntu*** por ***iaas-dsi16*** de la dirección 127.0.1.1
  * Actualizamos el software: sudo apt update  &  sudo apt upgrade
  * Reiniciamos el sistema: sudo reboot
  
  ![cat /etc/hosts en Virtual][IpMVenMv]

* En tercer lugar, vamos a incluir a la MV en la listas de hosts de la máquina local, de manera que no tengamos que recordar la dirección IP de la MV. Para ello haremos:

  * Ejecutamos el comando en la máquina local: sudo vi /etc/hostname
  * Añadimos la dirección IP de la máquina virtual (***10.6.130.26***) y su nombre ***iaas-dsi16***
 
  ![cat /etc/hosts en Local][IpMVenLC]
  
* Además he completado el siguiente curso: **[Curso introductorio GitHub](https://lab.github.com/githubtraining/introduction-to-github)**

  * El repositorio de muestra está en: **[Mi cuenta de GitHub](https://github.com/alu0101205908/github-slideshow)**

* Adicionalmente, he utilizado un simulador online para ver como quedaba el presente fichero en Markdown. **[Markdown Online](https://jbt.github.io/markdown-editor/)**

## Conclusión:

* En esta práctica hemos configurado el que va a ser nuestro medio de trabajo para la presente asignatura. Gracias al tutorial guiado que nos ha facilitado el profesor ha sido bastante sencillo de realizar dicha configuración. Hemos hecho varias labores que ya hemos realizado en otras asignaturas, como trabajar con la shell de Unix para configurar ficheros del sistema e instalar paquetes, trabajar con el sistema de control de versiones Git y con GitHub. Con esta última herramienta, hemos aprendido la funcionalidad de GitHub Pages, un generador de páginas con dominio .github.io que se autogeneran a partir de un fichero en Markdown. Por otra parte, he hecho un curso de GitHub, que pese a que fue de corta duración me sirvió para aprender mucho acerca de la plataforma, dado que yo ya era usuario de GitHub, pero solo lo utilizaba para publicar mis pequeños proyectos o ideas a partir de un repositorio desde mi máquina. 


[Numeracion]: images/numeracion.JPG "Numeración"
[IP]: images/IP.JPG "IP"
[UsuarioIP]: images/usuariosIP.JPG "Usuario@IP"
[Settings1]: images/settings1.JPG "Ajustes"
[Settings2]: images/settings2.jpg "New SSH"
[Settings3]: images/settings3.jpg "New SSH key"
[gitConfig]: images/gitConfig.JPG "Git config"
[cambioPrompt]: images/cambioPrompt.JPG "Prompt cambiado"
[promptRama]: images/promptRama.JPG "Prompt rama"
[nvm]: images/nvmVersion.JPG "Version nvm"
[node&npm]: images/node&npmVersion.JPG "Version de node y npm"
[hostName]: images/hostname.JPG "cat /etc/hostname en MV"
[IpMVenMv]: images/ipMV.JPG "cat /etc/hosts en Virtual"
[IpMVenLC]: images/ipML.JPG "cat /etc/hosts en Local"
