
# dispatch-proxy

A SOCKS5/HTTP proxy que equilibra el tráfico entre varias conexiones a Internet.

_Works on <b>Mac OS X</b>, <b>Windows</b> and <b>Linux</b>._

**Instrucciones de instalación detalladas:**

- Windows: [imgur album](http://imgur.com/a/0snis)
- Mac OS X: [imgur album](http://imgur.com/a/TSD5F)

## Instalación


Deberá tener Node.JS >= 0.10.0 instalado en su sistema.

```
$ npm install -g dispatch-proxy
```

Actualizar

```
$ npm update -g dispatch-proxy
```
## Justificación

A menudo te encuentras con múltiples conexiones a Internet sin usar, ya sea una suscripción móvil 3G/4G o un punto de acceso wifi gratuito, que tu sistema no te permite usar junto con la principal.

Por ejemplo, mi residencia me proporciona acceso a Internet por cable e inalámbrico. Ambos tienen un límite de velocidad de carga/descarga de 1200 kB/s, pero pueden ejecutarse simultáneamente a toda velocidad. Mi acceso a Internet móvil también me proporciona una velocidad de carga/descarga de 400kB/s.

Combine todo esto con `dispatch` y un administrador de descargas por subprocesos y obtendrá un límite de velocidad de carga y descarga de 2800 kB/s, que es considerablemente mejor :)

## Casos de uso

Las posibilidades son infinitas:

- combine tantas redes Wi-Fi/Ethernet/3G/4G como tenga acceso en una gran conexión con carga equilibrada,
- Úselo junto con un administrador de descargas en subprocesos, combinando efectivamente la velocidad de múltiples conexiones en descargas de un solo archivo,
- cree dos proxies, asigne a cada uno su propia interfaz y ejecute dos aplicaciones simultáneamente que usen una interfaz diferente (por ejemplo, para equilibrar la carga/descarga),
- cree un proxy de punto de acceso en casa que se conecte a través de Ethernet y su tarjeta 4G para todos sus dispositivos móviles,
- etc.


## Inicio rápido

El módulo proporciona una sencilla utilidad de línea de comandos llamada `dispatch`.

```
$ dispatch start
```

Inicie un servidor proxy SOCKS en `localhost:1080`. Simplemente agregue esta dirección como un proxy SOCKS en la configuración de su sistema y su tráfico se equilibrará automáticamente entre todas las conexiones de Internet disponibles.


## Uso

```
$ dispatch -h

  Usage: dispatch [options] [command]

  Commands:

    list                   list all available network interfaces
    start [options]        start a proxy server

  Options:

    -h, --help     output usage information
    -V, --version  output the version number
```

```
$ dispatch start -h

  Usage: start [options] [addresses]

  Options:

    -h, --help      output usage information
    -H, --host <h>  which host to accept connections from (defaults to localhost)
    -p, --port <p>  which port to listen to for connections (defaults to 8080 for HTTP proxy, 1080 for SOCKS proxy)
    --http          start an http proxy server
    --debug         log debug info in the console
```

## Ejemplos

```
$ dispatch start --http
```
Inicie un servidor proxy HTTP escuchando en `localhost:8080`, enviando conexiones a todas las direcciones locales IPv4 no internas.


```
$ dispatch start 10.0.0.0 10.0.0.1
```
Envíe conexiones solo a las direcciones locales `10.0.0.0` y `10.0.0.1`.


```
$ dispatch start 10.0.0.0@7 10.0.0.1@3
```
Envíe conexiones a `10.0.0.0` 7 veces de cada 10 y a '10.0.0.1' 3 veces de cada 10.
