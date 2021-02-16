# PRÁCTICA 1: Configuración de la máquina virtual en el IaaS

En esta primera práctica hemos configurado nuestro entorno de trabajo para la asignatura de Desarrollo de Sistemas Informáticos. En líneas generales, lo que se ha hecho es configurar la máquina virutal que nos proporciona el IasS (Infraestructura como servicio) de la Universidad de La Laguna, modelando el ecosistema que utilizaremos en esta asignatura.

## Tareas iniciales:

* Para empezar, debemos de tener instalado el software de VPN de la Universidad de La Laguna, para emular que estamos conectados a su red, y así poder acceder a los servicios del IaaS. En nuestro caso, ya tenemos configurada la VPN, dado que ya lo hemos necesitado para otras asignaturas. Una vez activada la VPN de la ULL, nos dirigimos a **[IaaS ULL](https://iaas.ull.es/ovirt-engine/sso/login.html)**, e introducimos nuestras credenciales para poder acceder a nuestro pool de máquinas. 

  * (***En caso de no tener activa la VPN de la ULL, no podremos acceder al link del portal del IaaS***). 

* Una vez dentro del pool, debemos ejecutar la máquina de esta asignatura (**DSI**), y obtendremos nuestra numeración (***16***), y la IP de nuestra máquina (***10.6.130.26***) 

![Numeración][numeracion]
![IP][IP]

* A continuación, ya podemos dirigirnos a nuestra máquina Linux, y en la consola accederemos por SSH a nuestra máquina, dado que conocemos el nombre del usuario (***usuario***) y la IP. 

![Usuario@IP][UsuarioIP]

  * (***Nos saldrá un mensaje al que deberemos respnder con "yes" e intro, y nos pedirá una cntraseña, que será "usuario"***)
  
* Una vez aceptado el mensaje, deberemos cambiar la contraseña

En caso de no tener el software de VPN instalado, se recomienda leer la siguiente documentación: **[VPN ULL](https://www.ull.es/servicios/stic/2020/12/01/servicio-de-vpn-de-la-ull/)**



For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/ULL-ESIT-INF-DSI-2021/ull-esit-inf-dsi-20-21-prct01-iaas-alu0101205908.github.io/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.


[Numeracion]: images/numeracion.jpg "Numeración"
[IP]: images/ip.jpg "IP"
[UsuarioIP]: images/usuarioIP.jpg "Usuario@IP"
