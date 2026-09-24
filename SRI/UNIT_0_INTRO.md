Comprobación de red (ip a): Se consultan las interfaces de red del sistema Ubuntu. Se observa la interfaz del bucle local (lo), la interfaz de red NAT enp0s3 (IP 10.0.2.15), y una interfaz en adaptador solo-anfitrión enp0s8 (IP 192.168.56.101).
Actualización del sistema (sudo apt update y sudo apt upgrade): Se actualizan los índices de paquetes del sistema operativo. El sistema indica que no hay actualizaciones pendientes instalables por políticas de phasing.

Instalación de SSH (sudo apt install openssh-server): Se solicita la instalación del servidor SSH en Ubuntu.
Confirmación e instalación: Se aceptan las dependencias necesarias (ncurses-term, openssh-sftp-server, ssh-import-id) y se realiza la descarga y configuración de los paquetes del servidor OpenSSH.

Verificación de estado (sudo systemctl status ssh): Se revisa el servicio SSH, que figura como inactivo (inactive (dead)) y deshabilitado (disabled).
Error de sintaxis (sudo systemctl enable): Ocurre un error por falta de argumentos (Too few arguments) al omitir el nombre del servicio.
Habilitación e inicio (sudo systemctl enable --now ssh): Se activa el servicio SSH para que se inicie automáticamente en el arranque y se pone en marcha de forma inmediata.

Conexión remota por SSH: Desde la consola de Windows, se establece conexión SSH hacia la máquina virtual ejecutando ssh raul@192.168.56.101.
Aceptación de la huella digital: Se confirma la autenticidad del host escribiendo yes para añadir la clave ED25519 al archivo known_hosts de Windows e introduciendo la contraseña del usuario.
Acceso y comprobación de repositorios: Una vez dentro de la sesión de Ubuntu vía SSH, se ejecutan sudo apt update y sudo apt upgrade.
Instalación de Git y GitHub CLI (sudo apt install git gh): Se inicia la instalación de Git junto con la herramienta de consola de GitHub (gh).

Finalización de instalación de Git y GH: Se completa el proceso de desempaquetado y configuración de los paquetes git y gh.
Verificación de versiones (git --version / gh --version): Se confirma que Git (versión 2.53.0) y GH (versión 2.46.0) están correctamente instalados.
Inicio de sesión en GitHub (gh auth login): Se arranca el asistente de autenticación seleccionando GitHub.com, protocolo HTTPS y la opción de autenticación vía navegador web.

Autenticación en GitHub CLI: Tras cancelar un primer intento, se reintenta el comando gh auth login completando el flujo con el código de un solo uso (CD1E-A6FC), logrando la autenticación como raulguadix-sys.
Creación e inicialización del repositorio local:
Se crea el directorio de trabajo con mkdir ASIR2_2627 y se entra en él (cd ASIR2_2627).
Se inicializa el repositorio local mediante git init.
Se intenta redactar la primera línea del archivo README con echo "# ASIR2_2627" > README.md.

Corrección de sintaxis y creación de archivo: Tras cancelar un comando con errores de sintaxis (^C), se genera correctamente el archivo README.md.
Primer intento de commit: Se añade el archivo al área de preparación con git add . y se ejecuta git commit -m "Primer commit". Git rechaza el commit por falta de configuración de identidad del autor.
Configuración del usuario de Git: Se definen las credenciales globales:
git config --global user.name "Raúl Caño Puerto"


git config --global user.email "raulguadix@gmail.com"


Creación exitosa del commit: Se ejecuta nuevamente git commit -m "Primer commit", registrando los cambios en la rama master.
Intento fallido de creación del repositorio remoto: Se ejecuta gh repo create ASIR2_2627 --public --source. --remote=origin --push, generando un error de sintaxis en el parámetro --source. (por un punto sobrante).

Publicación del repositorio en GitHub: Se corrige el comando ejecutando gh repo create ASIR2_2627 --public --source=. --remote=origin --push.
Resultado: Se crea con éxito el repositorio público raulguadix-sys/ASIR2_2627 en GitHub, se vincula el origen remoto origin y se sube el código local mediante el push inicial de la rama master.

