<p align="center"><picture><source media="(prefers-color-scheme: dark)" srcset="marca/loganos-branco.svg"><img src="marca/loganos-preto.svg" width="96" alt="LoganOS"></picture></p>

# LoganOS

[English](README.md) · [Português](README.pt-BR.md) · **Español**

Un panel para home lab en un solo archivo Python. Accesos a tus servicios, monitor del sistema, discos con la salud por SMART, eventos de seguridad, notificaciones, copias de seguridad y pequeñas apps integradas (Notas, Links, Cámara). Sin pip, sin Docker, sin base de datos: solo la biblioteca estándar de Python.

<p align="center"><img src="imagens/inicio.png" alt="LoganOS"></p>

<p align="center"><img src="imagens/monitor.png" width="72%" alt="Monitor"> <img src="imagens/celular.png" width="24%" alt="LoganOS"></p>

<p align="center"><img src="imagens/entrada.png" width="48%" alt="Sign in"> <img src="imagens/ajustes.png" width="48%" alt="Settings"></p>

## Requisitos

- Linux con systemd. Probado en **Debian 13 (x86_64)**. Debian 12, Ubuntu 24.04 y Raspberry Pi OS deberían funcionar, pero todavía no se probaron.
- Python 3.11 o más nuevo (ya viene en esos sistemas).
- Acceso de root para instalar.

## Instalar

```sh
sudo mkdir -p /opt/loganos
sudo curl -fsSL -o /opt/loganos/loganos.py https://github.com/erisfernandes/LoganOS/releases/latest/download/loganos.py
sudo python3 /opt/loganos/loganos.py --instalar
```

Abre `http://<ip-del-servidor>:8092` y crea tu cuenta. El idioma sigue al navegador (español, inglés o portugués) y se puede cambiar en Ajustes.

## Actualizar

Desde la página (Ajustes, Seguridad, Versiones) o en la terminal:

```sh
sudo python3 /opt/loganos/loganos.py --atualizar
```

La actualización descarga la última release y solo la instala si el SHA-256 coincide con el `loganos.py.sha256` publicado. Si la versión nueva no arranca, vuelve sola la anterior.

## Comprobar una descarga

Cada release está firmada con [minisign](https://jedisct1.github.io/minisign/). La clave pública (id 407236916ABFC1EF) es:

```
RWTvwb9qkTZyQBKWsZ2B8t/Fbq7kBgZ9Feuvr66yYaP0Y6aqZhf9XcG6
```

Con `loganos.py` y `loganos.py.minisig` de la release en la misma carpeta:

```sh
minisign -Vm loganos.py -P RWTvwb9qkTZyQBKWsZ2B8t/Fbq7kBgZ9Feuvr66yYaP0Y6aqZhf9XcG6
```

El panel hace la misma comprobación solo antes de instalar una actualización.

## Desinstalar

```sh
sudo python3 /opt/loganos/loganos.py --desinstalar
```

Pregunta antes de quitar nada y pregunta otra vez antes de borrar tus datos.

## Seguridad

- Hecho **solo para la red de casa y Tailscale**. Las solicitudes desde IP públicas se rechazan. No lo expongas a internet.
- En la red de casa la página usa HTTP sin cifrado. Para HTTPS, usa Tailscale (`--https`).
- El panel corre como un `DynamicUser` de systemd, sin privilegios, y no como root.
- Tres ayudantes pequeños corren como root, cada uno con una lista fija de acciones. Nada escrito en la página se vuelve parte de un comando:
  - `loganos-servicos`: lee la lista de servicios, los puertos abiertos y los discos.
  - `loganos-ajudante`: lee la salud de los discos (SMART), las actualizaciones del sistema, las versiones, el resumen de Pi-hole y el estado del HTTPS.
  - `loganos-pedidos`: reinicia un servicio que falló, monta y desmonta discos USB, hace la copia de seguridad, actualiza LoganOS y el baúl de contraseñas opcional. La solicitud es solo un nombre de archivo, comprobado contra patrones fijos.
- Sin telemetría. Conexiones hacia internet, todas opcionales o a pedido: prueba de velocidad (Cloudflare), versiones nuevas (GitHub), ntfy.sh como respaldo de los avisos, comprobación del DNS (`www.google.com`) y las páginas que guardas en Links.

## Soporte

Solo por las [issues de GitHub](https://github.com/erisfernandes/LoganOS/issues), sin plazo de respuesta. Indica la versión, el sistema y el registro exportado.

## Licencia

[AGPL-3.0](LICENSE). © 2026 Eris Fernandes.
