# AEE. Bitácora III. Conexiones Empresariales Taller Técnico: Operación Escudo 

* **Módulo**: Sistemas Informáticos (0483)  
* **Unidad Didáctica 6**: Seguridad y Gestión de Recursos en Red  
* **Método de Entrega:** Repositorio GitHub (Documentación técnica en Markdown \+ Scripts de automatización)

### 1\. El Escenario: "La Defensa en Profundidad y el rastro digital"

En la administración de sistemas moderna, la invisibilidad es una de las mejores defensas, pero nunca debe ser la única. Hablamos constantemente del concepto de **Defensa en Profundidad (Defense in Depth)**. Esto significa que no podemos confiar únicamente en una contraseña fuerte o en un cortafuegos; necesitamos múltiples capas superpuestas. Si un atacante logra traspasar la primera barrera, debe encontrarse con una segunda, y luego con una tercera. Y lo que es más importante: si logra encontrar la puerta, vuestro servidor debe ser capaz de registrar y alertar de cada uno de sus movimientos.

Y es que, para que os hagáis una idea, un servidor Linux recién expuesto en la nube (ya sea en AWS, Azure o GC) tarda, de media, menos de 5 minutos en recibir su primer escaneo de red automatizado. Existen redes enteras de bots rastreando Internet 24/7 en busca de puertos SSH abiertos y vulnerabilidades conocidas.

Ya no serás un usuario convencional; actuarás como **Administrador de Sistemas (SysAdmin)** en medio de un despliegue crítico y con el reloj en contra. El objetivo es claro: fortificar el sistema mediante técnicas de *Hardening*, levantar un muro de fuego *stateful* (*Firewall*) y automatizar la vigilancia de los registros antes de que acabe vuestro turno.

Recordad el pilar fundamental de los sistemas basados en Unix: "**Todo es un fichero**". Desde la tarjeta de red virtual, pasando por la memoria RAM, hasta llegar a la configuración del firewall y los registros de seguridad. Entender esta arquitectura es la llave maestra para dominar cualquier servidor.

### 2\. Fase de Investigación: Comprendiendo el corazón del sistema

Antes de realizar cambios a lo loco en un entorno de producción, un buen administrador debe investigar y fundamentar sus decisiones. La improvisación técnica suele derivar en fallos de seguridad críticos o en servidores inoperativos. Utilizad vuestro acceso a las bases de datos académicas \[1\] para dotar de base científica y metodológica a vuestro trabajo:

* **Reto de Investigación 1**. Anatomía de Syslog. Profundiza en el estándar Syslog, el sistema de mensajería vital de Linux. Investiga cómo el sistema clasifica los eventos cruzando dos variables: "Facilidad" (*Facility*, es decir, qué parte del sistema genera el log, como auth, cron o daemon) y "Prioridad" (*Severity*, desde *debug* hasta *emerg*).

  El sistema de log (Syslog) almacena mensajes y comandos. Una instalación debe de imprimir el Syslog periódicamente para verificar si existen problemas. Además, se puede utilizar en aplicaciones y por programadores del sistema. Syslog consiste en:

* Todos lo mensajes publicados por marcos WTL  
* Todos los mensajes introducidos por comandos del operador de LOG  
* Generar el log hard-copy  
* Los mensajes dirigidos a Syslog desde cualquier componente o programa del sistema

  \[4\] \[8\]

  * Además, responde a esto: ¿Por qué es una negligencia grave que el archivo */var/log/auth.log* tenga permisos de lectura para usuarios no privilegiados?

    La carpeta “/var/log/”, contiene toda la lista de archivos logs del sistema operativo, es decir, se almacenan todos los registros del sistema. 

    El archivo */var/log/auth.log* contiene los log de autentificación, En este log se registran los login y demás comandos que se producen en el sistema. Conexiones al sistema incluidos los intentos fallidos y los accesos como root. Autorizaciones que hace el sistema, logins de usuarios y de software. Información sobre eventos de autenticación de usuarios

    Por lo anteriormente mencionado, es una negligencia que el archivo /var/log/auth.log tenga permisos de lectura para usuarios no privilegiados. Porque dichos usuarios podrán ver como el “historial” de comandos utilizados y los fallos que se han producido, de hecho se expone información sensible que facilita la entrada y el movimiento lateral de un atacante. \[6\] \[8\]

  * ¿Qué información específica (como PIDs, nombres de usuario o direcciones IP) diferencia un intento fallido de conexión remota *SSH* de un simple fallo de contraseña de un usuario local frente a la pantalla?

    La principal diferencia se encuentra en la IP, porque cuando el servicio que gestiona la identificación, la fuente de conexión y el método de login no llegaron a ser los estándares, se registran de forma diferente. \[7\]\[8\]

* **Reto de Investigación 2**. Cumplimiento y Log Management. Busca en **Dialnet** o **Semantic Scholar** artículos sobre *Log Management* (Gestión centralizada de registros). A nivel empresarial y legal (piensa en el RGPD en España), ¿qué ventajas vitales ofrece enviar y custodiar los logs en un servidor externo seguro en lugar de mantenerlos dispersos e indefensos en la propia máquina que podría ser vulnerada?

  Principalmente se tienen las siguientes ventajas:

  * Capacidad de análisis forense y determinación del alcance: se deben de disponer de los logs centralizados, porque si no el atacante podría borrarlos para ocultar su rastro.  
  * Integridad y seguridad mediante cifrado:   
  * Monitorización y alertas en tiempo real:  
  * Cumplimiento normativo y legal:  
  * Visibilidad centralizada y auditoría:  
  * Protección contra el borrado accidental o intencionado:

   \[1\]\[8\]\[9\]

* **Documentación obligatoria**. Crea un archivo **README.md** en la raíz de vuestro repositorio GitHub. La primera sección debe titularse "Fundamentos de Seguridad y Auditoría". En ella, debéis explicar todos estos conceptos analizados con vuestras propias palabras (nada de copiar y pegar). Por supuesto, debéis respaldar vuestras afirmaciones citando al menos dos fuentes reales y accesibles siguiendo estrictamente el manual de estilo IEEE \[2\].

### 

### Referencias para la consulta

\[1\] W. Acosta Lugo, *Guía de uso de BBDD Académicas para Ciclos Formativos*, Sevilla, España: Departamento de Informática, 2026\. Disponible en: [https://drive.google.com/file/d/1Zg4LNDAs55OgEK1gmqbGx8NZyc1CdJjM/view?usp=sharing](https://drive.google.com/file/d/1Zg4LNDAs55OgEK1gmqbGx8NZyc1CdJjM/view?usp=sharing).

\[2\] IEEE, *IEEE Editorial Style Manual for Authors*, IEEE Periodicals, 2023\. \[En línea\]. Disponible en: [https://journals.ieeeauthorcenter.ieee.org/your-role-in-article-production/ieee-editorial-style-manual/](https://journals.ieeeauthorcenter.ieee.org/your-role-in-article-production/ieee-editorial-style-manual/)

\[3\] Canonical Ltd., "Ubuntu Server documentation," Ubuntu Documentation, 2025\. \[En línea\]. Disponible en: [https://ubuntu.com/server/docs/explanation/intro-to/security/](https://ubuntu.com/server/docs/explanation/intro-to/security/)

\[4\] M. B. Alonso Alegre Díez, "Gestión de Logs," Trabajo Fin de Máster, Universidad Internacional de La Rioja (UNIR), 2016\. \[En línea\]. Disponible en: [https://reunir.unir.net/bitstream/handle/123456789/3618/ALONSO-ALEGRE%20DIEZ%2C%20MARIA%20BEGO%C3%91A.pdf](https://reunir.unir.net/bitstream/handle/123456789/3618/ALONSO-ALEGRE%20DIEZ%2C%20MARIA%20BEGO%C3%91A.pdf)

\[5\] S. McClure, J. Scambray y G. Kurtz, *Hacking Exposed: Network Security Secrets & Solutions*, 3ª ed. Nueva York, NY, EE. UU.: McGraw-Hill Education, 2001\. Disponible en: [https://github.com/jwx0539/hackingLibrary/blob/master/McGraw.Hill.Hacking.Exposed.Network.Security.Secrets.And.Solutions.3rd.Edition.Sep.2001.ISBN.0072193816.pdf](https://github.com/jwx0539/hackingLibrary/blob/master/McGraw.Hill.Hacking.Exposed.Network.Security.Secrets.And.Solutions.3rd.Edition.Sep.2001.ISBN.0072193816.pdf)

\[6\] "var/log/auth.log permissions," Unix & Linux Stack Exchange, 7 de diciembre de 2017\. \[En línea\]. Disponible en: [https://unix.stackexchange.com/questions/409660/var-log-auth-log-permissions](https://unix.stackexchange.com/questions/409660/var-log-auth-log-permissions). \[Accedido: 17-abr-2026\].

\[7\] "How to Find Failed SSH Login Attempts in Linux," TecMint. \[En línea\]. Disponible en: [https://www.tecmint.com/find-failed-ssh-login-attempts-in-linux/](https://www.tecmint.com/find-failed-ssh-login-attempts-in-linux/). \[Accedido: 17-abr-2026\].

\[8\] W. Acosta Lugo, *\[DAM/DAW\_SI\]AEE.BitacoraIIIUD06y7*, Sevilla, España: Departamento de Informática, 2026\. Disponible en: [https://docs.google.com/document/d/1bORxj6oclMMasHh4iwT7HOR4yGe4jZEizDusdSxpavM/edit?usp=sharing](https://docs.google.com/document/d/1bORxj6oclMMasHh4iwT7HOR4yGe4jZEizDusdSxpavM/edit?usp=sharing)

\[9\] S. Fernández Benito, "Gestión de vulnerabilidades en entornos Cloud," Trabajo Final de Máster, Universitat Oberta de Catalunya (UOC), 2 de junio de 2020\. \[En línea\]. Disponible en: [https://openaccess.uoc.edu/server/api/core/bitstreams/ae6ab0d0-bf78-465c-a115-ca2a72a4bc70/content](https://openaccess.uoc.edu/server/api/core/bitstreams/ae6ab0d0-bf78-465c-a115-ca2a72a4bc70/content). \[Accedido: 17-abr-2026\].