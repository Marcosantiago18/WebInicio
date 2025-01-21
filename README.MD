## Manual para generar claves nuevas de ssh

### 1.Comprobación de clves SSH existentes
En primer lugar comprobamos si hay claves existentes.

1.Abrimos git bash.

2.Nos dirigimos a la la carpeta oculta ~/.ssh para ver si existen las claves.

    '''bash
    ls -al ~/.ssh
    #Nos deberia mostrar las claves
    '''

3.Dentro del directorio nos deberia mostrar algo como esto (id_ed25519 | id_ed25519.pub) si nuestras claves ssh existen.

4.Si nos indica que ~/.ssh no existe o dentro de esta no se encuentran las claves deberemos generar una nueva clave SSH.

### 2.Generar una nueva clave SSH 
    
1.Abrimos git bash.

2.Escribimos lo siguiente, teniendo encuenta que debes poner tu correo de GitHub.

    '''bash
        ssh-keygen -t ed25519 -C "your_email@example.com"
    '''

Esto nos deberia devolver algo como esto, debermos dar enter a lo que nos pregunta:

    '''bash
        Generating public/private ed25519 key pair.
        Enter file in which to save the key (/c/Users/YOU/.ssh/id_edXXXXX):
        Created directory '/c/Users/YOU/.ssh'.
        Enter passphrase for "/c/Users/YOU/.ssh/id_edXXXXX" (empty for no passphrase):
        Enter same passphrase again:
        Your identification has been saved in /c/Users/YOU/.ssh/id_edXXXXX
        Your public key has been saved in /c/Users/YOU/.ssh/id_edXXXXX.pub
        The key fingerprint is:
        your_email@example.com
        The key's randomart image is:
        +--[EDXXXXX XXX]--+
        | oOo.O+.         |
        | +o=+.*o         |
        |. .oBoE .        |
        | . +.X B         |
        |    @ B S        |
        |   = O =         |
        |    + o o        |
        |     . o .       |
        |      o..        |
        +----[XXXXX]-----+
    '''

### 3.Agragar las claves SSH al ssh-agent
1.En una ventana de PowerSell ejecutada como administrador ejecutaremos lo siguiente.

    '''bash
        Get-Service -Name ssh-agent | Set-Service -StartupType Manual
        Start-Service ssh-agent
    '''

2.Luego agregaremos la clave al aah-agent ejecutando lo siguiente:

    '''bash
        ssh-add c:/Users/YOU/.ssh/id_ed25519
    '''

3.Procederemos a agregar nuestra clave publica a GitHub

### 4.Agregar nuestra clave publica a GitHub
1.Copiamos la clave publica en el portapapeles

    '''bash
        cat ~/.ssh/id_ed25519.pub | clip
        #Copiamos lo que nos devuelve por pantalla
    '''
2.En la esquina superior izquierda en GitHub hacemos clic en la foto de perfil y hacemos clic en **Configuración**

3.En la seccion de "Acceso" hacemos clic en **Claves SSH y GPG**

4.Hacemos clic en **Nueva clave SSH** o **Agregar clave SSH** 

5.Se nos abrira una pestaña. En el **Titulo**, agrege un nombre reconocer el dispositivo de la clave publica.

6.En el **tipo de clave**, debe de poner si es autenticación o firma  

7.En el campo **Clave** tiene que pegar la clave pública
8.Por ultimo, haga clic en **Agregar clave SSH**                       

Y así tendriamos nuestra nueva clave ssh generada y agregada a nuestro GitHub.
