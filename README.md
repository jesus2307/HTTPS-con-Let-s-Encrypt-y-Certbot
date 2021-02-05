# IAW-Pr-ctica-HTTPS-

<h1 id="práctica-https-con-lets-encrypt-y-certbot"><span class="header-section-number">1</span> Práctica: HTTPS con Let’s Encrypt y Certbot</h1>
<p>En esta práctica vamos a habilitar el protocolo <a href="https://es.wikipedia.org/wiki/Protocolo_seguro_de_transferencia_de_hipertexto">HTTPS</a> en un sitio web <a href="https://wordpress.org">WordPress</a> que se estará ejecutando en una instancia EC2 de <a href="https://aws.amazon.com/es/ec2/">Amazon Web Services (AWS)</a>.</p>
<h2 id="conceptos-básicos"><span class="header-section-number">1.1</span> Conceptos básicos</h2>
<h3 id="qué-es-https"><span class="header-section-number">1.1.1</span> ¿Qué es HTTPS?</h3>
<p><a href="https://es.wikipedia.org/wiki/Protocolo_seguro_de_transferencia_de_hipertexto">HTTPS</a> (<em>Hyptertext Transfer Protocol Secure</em>) o protocolo seguro de transferencia de hipertexto, es un protocolo de la capa de aplicación basado en el protocolo HTTP, destinado a la transferencia segura de datos de hipertexto. (Fuente: <a href="https://es.wikipedia.org/wiki/Protocolo_seguro_de_transferencia_de_hipertexto">Wikipedia</a>)</p>
<p>Para poder habilitar el protocolo <a href="https://es.wikipedia.org/wiki/Protocolo_seguro_de_transferencia_de_hipertexto">HTTPS</a> en un sitio web es necesario obtener un <strong>certificado de seguridad</strong>. Este certificado tiene que ser emitido por una <strong>autoridad de certificación</strong> (AC). En esta práctica vamos a obtener un certificado para un dominio de la Autoriidad de Certificación <a href="https://letsencrypt.org">Let’s Encrypt</a>.</p>
<h3 id="qué-es-lets-encrypt"><span class="header-section-number">1.1.2</span> ¿Qué es Let’s Encrypt?</h3>
<p><a href="https://letsencrypt.org">Let’s Encrypt</a>​ es una autoridad de certificación que se puso en marcha el 12 de abril de 2016 y que proporciona <a href="https://es.wikipedia.org/wiki/X.509">certificados X.509</a> <strong>gratuitos</strong> para el cifrado de seguridad de nivel de transporte (<a href="https://es.wikipedia.org/wiki/Seguridad_de_la_capa_de_transporte">TLS</a>) a través de un proceso automatizado diseñado para eliminar el complejo proceso actual de creación manual, la validación, firma, instalación y renovación de los certificados de sitios web seguros. (Fuente: <a href="https://es.wikipedia.org/wiki/Let%27s_Encrypt">Wikipedia</a>)</p>
<h3 id="cómo-funciona-lets-encrypt"><span class="header-section-number">1.1.3</span> Cómo funciona Let’s Encrypt</h3>
<p>Se recomienda la lectura de la sección <strong>Cómo Funciona Let’s Encrypt</strong> de la <a href="https://letsencrypt.org/es/how-it-works/">documentación oficial</a>.</p>
<h3 id="qué-es-certbot"><span class="header-section-number">1.1.4</span> ¿Qué es Certbot?</h3>
<p>Para poder obtener un certificado de <a href="https://letsencrypt.org">Let’s Encrypt</a> para un dominio de un sitio web es necesario demostrar que se tiene control sobre ese dominio. Para realizar esta tarea es necesario utilizar un cliente del <a href="https://en.wikipedia.org/wiki/Automated_Certificate_Management_Environment">protocolo ACME (Automated Certificate Management Environment)</a>. El cliente ACME recomendado para esta tarea es <a href="https://certbot.eff.org/">Certbot</a> porque es fácil de usar, tiene soporte para muchos sistemas operativos y dispone de una excelente documentación.</p>

# 1.3 Tareas a realizar

+ Crear una instancia EC2 en Amazon Web Services (AWS).
![imagen](https://github.com/jesus2307/IAW-Pr-ctica-HTTPS-/blob/main/imagen/6.PNG "imagen")
Cuando esté creando la instancia deberá configurar los puertos que estarán abiertos para poder conectarnos por SSH y para poder acceder por HTTP/HTTPS.

* SSH (22/TCP)
* HTTP (80/TCP)
* HTTPS (443/TCP)
![imagen](https://github.com/jesus2307/IAW-Pr-ctica-HTTPS-/blob/main/imagen/amzon.PNG "imagen")
+ Registrar un nombre de dominio en algún proveedor de nombres de dominio gratuito. Por ejemplo, puede hacer uso de Freenom.
![imagen](https://github.com/jesus2307/IAW-Pr-ctica-HTTPS-/blob/main/imagen/1.png "imagen")

+ Obtener la dirección IP pública de su instancia EC2 en AWS.
![imagen](https://github.com/jesus2307/IAW-Pr-ctica-HTTPS-/blob/main/imagen/5.PNG "imagen")

+ Configurar los registros DNS del proveedor de nombres de dominio para que el nombre de dominio de ha registrado pueda resolver hacia la dirección IP pública de su instancia EC2 de AWS.
![imagen](https://github.com/jesus2307/IAW-Pr-ctica-HTTPS-/blob/main/imagen/2.png "imagen")

+ A continuación, instala wordpress:
![imagen](https://github.com/jesus2307/IAW-Pr-ctica-HTTPS-/blob/main/imagen/Captura55.PNG "imagen")

+ Instalar y configurar el cliente ACME Certbot en su instacia EC2 de AWS, siguiendo los pasos de la documentación oficial.
![imagen](https://github.com/jesus2307/IAW-Pr-ctica-HTTPS-/blob/main/imagen/4.png "imagen")
<p>Una vez llegado hasta este punto tendríamos nuestro sitio web con <strong>HTTPS habilidado y todo configurado para que el certificado se vaya renovando automáticamente</strong>.</p>
<p>Con el siguiente comando podemos comprobar que hay un temporizador en el sistema encargado de realizar la renovación de los certificados de manera automática.</p>
<pre><code>systemctl list-timers</code></pre>

wp search-replace 'http://la ip publica' 'https://nombre del dominio'
![imagen](https://github.com/jesus2307/IAW-Pr-ctica-HTTPS-/blob/main/imagen/Captura22222.PNG "imagen")
# Este seria el resultado:

![imagen](https://github.com/jesus2307/IAW-Pr-ctica-HTTPS-/blob/main/imagen/result.PNG "imagen")
