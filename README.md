# hello-world
my first repository, i'm happy

i dont know what to say

####Configura tus llaves SSH en local
Primer paso: Generar tus llaves SSH. Recuerda que es muy buena idea proteger tu llave privada con una contraseña.

ssh-keygen -t rsa -b 4096 -C "tu@email.com"
Segundo paso: Terminar de configurar nuestro sistema.

En Windows y Linux:

#### Encender el "servidor" de llaves SSH de tu computadora:
eval $(ssh-agent -s)

#### Añadir tu llave SSH a este "servidor":
ssh-add ruta-donde-guardaste-tu-llave-privada
En Mac:

#### Encender el "servidor" de llaves SSH de tu computadora:
eval "$(ssh-agent -s)"

Si usas una versión de OSX superior a Mac Sierra (v10.12)
debes crear o modificar un archivo "config" en la carpeta
de tu usuario con el siguiente contenido (ten cuidado con
las mayúsculas):
Host *
        AddKeysToAgent yes
        UseKeychain yes
        IdentityFile ruta-donde-guardaste-tu-llave-privada

Añadir tu llave SSH al "servidor" de llaves SSH de tu
computadora (en caso de error puedes ejecutar este
mismo comando pero sin el argumento -K):
ssh-add -K ruta-donde-guardaste-tu-llave-privada

#### Conexión a GitHub con SSH
Luego de crear nuestras llaves SSH podemos entregarle la llave pública a GitHub para comunicarnos de forma segura y sin necesidad de escribir nuestro usuario y contraseña todo el tiempo.

Para esto debes entrar a la Configuración de Llaves SSH en GitHub, crear una nueva llave con el nombre que le quieras dar y el contenido de la llave pública de tu computadora.

Ahora podemos actualizar la URL que guardamos en nuestro repositorio remoto, solo que, en vez de guardar la URL con HTTPS, vamos a usar la URL con SSH:

`git remote set-url origin url-ssh-del-repositorio-en-github`

#### Tags y versiones en Git y GitHub
Los tags o etiquetas nos permiten asignar versiones a los commits con cambios más importantes o significativos de nuestro proyecto.

Comandos para trabajar con etiquetas:

- Crear un nuevo tag y asignarlo a un commit: git tag -a nombre-del-tag id-del-commit.
- Borrar un tag en el repositorio local: git tag -d nombre-del-tag.
- Listar los tags de nuestro repositorio local: git tag o git show-ref --tags.
- Publicar un tag en el repositorio remoto: git push origin --tags.
- Borrar un tag del repositorio remoto: git tag -d nombre-del-tag y git push origin :refs/tags/nombre-del-tag.

`git config --global alias.superlog "log --graph --abbrev-commit --decorate --date=relative --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)' --all"`