# RClone-V2

Inicie sesión en su servidor SSH y abra la terminal. Ejecute el siguiente comando y el último Rclone estará instalado y listo para funcionar:
```
apt install zip unzip curl ; curl -O https://downloads.rclone.org/rclone-current-linux-amd64.zip ; unzip rclone-current-linux-amd64.zip ; cd rclone-*-linux-amd64 ; sudo cp rclone /usr/bin/ ; sudo chown root:root /usr/bin/rclone ; sudo chmod 755 /usr/bin/rclone ; rclone version
```
Ejecute el siguiente comando para abrir la configuración de Rclone:
```
rclone config
```
Todavía tenemos mucho más por hacer, ah, sí, de hecho. Ejecute el siguiente comando para contrarrestar los errores de montaje del fusor:
```
sudo ln -s /bin/fusermount /bin/fusermount3
```
Después de esto, primero debemos crear una carpeta en nuestro servidor que se usará para montar el almacenamiento VOD Crea uno si aún no tienes ninguno:
```
mkdir -p /VOD
```
Ahora que nuestra carpeta está creada, necesitamos montar nuestro directorio en esta carpeta como permanente. Para eso necesitamos configurar el comando de ejecución automática en crontab de la siguiente manera:

Los usuarios de Xtream UI o XUI ONE utilizan lo siguiente:
```
nano etc/crontab
```
Descanse, use esto para la configuración cron:
```
crontab -e
```
Verás algunos comandos ya configurados, ve al último y agrega el siguiente comando:
```
@reboot root rclone mount VOD: /VOD --copy-links --no-gzip-encoding --no-check-certificate --allow-other --allow-non-empty --umask 000 --vfs-cache-mode writes
```
Ahora presione CTRL+X + Y y presione Enter para guardar el archivo y reiniciar su sistema. Mientras el servidor esté activo nuevamente, verifique que su lista esté allí a través de algún FTP, disktop o el siguiente comando:
```
ls /VOD
```
Ahora deberías obtener una lista de directorios y archivos disponibles en tu terminal. Si no, las cosas no salieron bien, intente ejecutar el siguiente comando y verifique el directorio en algún software FTP como WinSCP .
