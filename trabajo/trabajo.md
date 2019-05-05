# Estudio de ataques informáticos. ¿Cómo actúan los piratas informáticos?
    Autores: Marina Hurtado Rosales y Nicolás Rodríguez Hernández-Carrillo
    Correos: marinahurtado@correo.ugr.es; nicolasrhc@correo.ugr.es
    
## Introducción
Desde la aparición de los primeros ordenadores en la primera mitad del siglo XX el panorama tecnológico ha avanzado de forma impresionante. Los sistemas informáticos se han ido multiplicando, y cada vez han adquirido más y más importancia. Esto, sumado al auge de Internet, nos permite compartir y acceder a información con mayor rapidez cada vez.
Hoy en día este avance tecnológico puede apreciarse en todos los niveles. El uso de la informática y de las redes de ordenadores ya no se reduce al ámbito laboral y profesional, sino que ha llegado a convertirse en un elemento cotidiano en la vida de las personas.
En un mundo ideal, toda esta información que se intercambia circularía de un extremo a otro de la comunicación con total seguridad, protegida en el tránsito de las influencias externas. La información se enviaría y llegaría con total integridad, sin que hubiese sido alterada externamente. Además, en este mundo ideal ninguna persona recibiría en contra de su voluntad información perjudicial. Sin embargo, este mundo ideal no existe.
La proliferación de los virus y códigos malignos y su rápida distribución a través de redes como Internet, así como los miles de ataques e incidentes de seguridad que se producen todos los años contribuyen a la concienciación de la importancia de la seguridad informática.
Pero, ¿qué es la seguridad informática? La **seguridad informática** se puede definir como el conjunto de medidas que impiden la ejecución de operaciones no autorizadas sobre un sistema o red informática, las cuales podrían tener una serie de efectos negativos en el sistema: daños sobre la información, compromiso de su confidencialidad, autenticidad o integridad, disminución del rendimiento de los equipos pertenecientes a la red, o bloqueo del acceso de usuarios registrados al sistema.
De esta manera se puede decir que algunos de los principales objetivos de la seguridad informática son:
 
- Minimizar y gestionar los riesgos, así como detectar los posibles problemas y amenazas a la seguridad.
- Garantizar la adecuada utilización de los recursos y aplicaciones del sistema.
- Limitar las pérdidas y conseguir la adecuada recuperación del sistema en caso de un incidente de seguridad.
- Cumplir con el marco legal y con los requisitos impuestos por los clientes en sus contratos.
Para poder alcanzar estos objetivos, dentro del proceso de gestión de la seguridad informática es necesario contemplar una serie de servicios o funciones de seguridad de la información:
 
- *Confidencialidad*: cada mensaje transmitido o almacenado en un sistema informático sólo podrá ser leído por su legítimo destinatario. Si dicho mensaje cae en manos de terceras personas, éstas no podrán acceder al contenido del mensaje original.
- *Autenticación*: garantiza que la identidad del creador de un mensaje o documento es legítima. También podemos hablar de la autenticidad de un equipo que se conecta a una red o intenta acceder a un determinado servicio.
- *Integridad*: garantiza que un mensaje o fichero no ha sido modificado desde su creación o durante su transmisión a través de una red informática.
- *No repudiación*: implementar un mecanismo probatorio que permita demostrar la autoría y envío de un determinado mensaje, de tal modo que el usuario que lo ha creado y enviado a través del sistema no pueda posteriormente negar esta circunstancia, situación que también se aplica al destinatario del envío.
- *Disponibilidad*: se debe diseñar un sistema lo suficientemente robusto frente a ataques e interferencias como para garantizar su correcto funcionamiento, de manera que pueda estar permanentemente a disposición de los usuarios que deseen acceder a sus servicios.
- *Autorización (control de acceso a equipos y servicios)*: controlar el acceso de los usuarios a los distintos equipos y servicios ofrecidos por el sistema informático, una vez superado el proceso de autenticación de cada usuario.
- *Auditabilidad*: permite registrar y monitorizar la utilización de los distintos recursos del sistema por parte de los usuarios que han sido previamente autenticados y autorizados.
- *Reclamación de origen*: permite probar quién ha sido el creador de un determinado mensaje o documento.
- *Reclamación de propiedad*: permite probar que un determinado documento o un contenido digital protegido por derechos de autor pertenece a un determinado usuario u organización que ostenta la titularidad de los derechos de autor.
- *Anonimato en el uso de los servicios*: En la utilización de determinados servicios dentro de las redes y sistemas informáticos también podría resultar conveniente garantizar el anonimato de los usuarios que acceden a los recursos y consumen determinados tipos de servicios, preservando de este modo su privacidad. Este servicio de seguridad, no obstante, podría entrar en conflicto con otros de los ya mencionados, como la autenticación o la auditoría del acceso a los recursos.
- *Protección a la réplica*: se trata de impedir la realización de “ataques de repetición” (replay attacks) por parte de usuarios maliciosos.
- *Confirmación de la prestación de un servicio o la realización de una transacción*: permite confirmar la realización de una operación o transacción, reflejando los usuarios o entidades que han intervenido en ésta.
- *Referencia temporal (certificación de fechas)*: mediante este servicio de seguridad se consigue demostrar el instante concreto en que se ha enviado un mensaje o se ha realizado una determinada operación.
- *Certificación mediante terceros de Confianza*: la realización de todo tipo de transacciones a través de medios electrónicos requiere de nuevos requisitos de seguridad, para garantizar la autenticación de las partes que intervienen, el contenido e integridad de los mensajes o la constatación de la realización de la operación o comunicación en un determinado instante temporal.
Para poder ofrecer algunos de estos servicios de seguridad se empieza a recurrir a la figura del “Tercero de Confianza”, organismo que se encarga de certificar la realización y el contenido de las operaciones y de avalar la identidad de los intervinientes, dotando de este modo a las transacciones electrónicas de una mayor seguridad jurídica.
Sin embargo, a pesar de todos los servicios de seguridad informática que pueda tener una red de ordenadores, ésta puede tener vulnerabilidades. Estas vulnerabilidades pueden ser puerta de entrada para intrusos.
## Atacantes
Estos intrusos que pueden aprovechar las vulnerabilidades de una red pueden ser de distintos tipos, y tener intenciones bien diferentes.
### Tipos de atacantes informáticos
- **Hackers:** Los hackers son intrusos que se dedican a estas tareas como pasatiempo y como reto técnico: entran en los sistemas informáticos para demostrar y poner a prueba su inteligencia y conocimientos de los entresijos de Internet, pero no pretenden provocar daños en estos sistemas. Sin embargo, el acceso no autorizado a un sistema informático se considera por sí mismo un delito en muchos países, puesto que aunque no se produzca ningún daño, se podría revelar información confidencial. Por otra parte los hackers pueden dejar "puertas traseras" en el sistema, las cuales podrían ser aprovechadas por usuarios maliciosos. 
- **Crackers (blackhats):** Los crackers son individuos con interés en atacar un sistema informático para obtener beneficios de forma ilegal o, simplemente, para provocar algún daño a la organización propietaria del sistema, motivados por intereses económicos, políticos, religiosos, etcétera.
- **Sniffers:** Los sniffers son individuos que se dedican a rastrear y tratar de recomponer y descifrar los mensajes que circulan por redes de ordenadores como Internet.
- **Phreakers:** Los phreakers son intrusos especializados en sabotear las redes telefónicas para poder realizar llamadas gratuitas. Los phreakers desarrollaron las famosas “cajas azules”, que podían emitir distintos tonos en las frecuencias utilizadas por las operadoras para la señalización interna de sus redes, cuando éstas todavía eran analógicas. 
- **Spammers:** Los spammers son los responsables del envío masivo de miles de mensajes de correo electrónico no solicitados a través de redes como Internet, provocando el colapso de los servidores y la sobrecarga de los buzones de correo de los usuarios. Además, muchos de estos mensajes de correo no solicitados pueden contener código dañino (virus informáticos) o forman parte de intentos de estafa realizados a través de Internet (los famosos casos de phishing).
- **Piratas informáticos:** Los piratas informáticos son los individuos especializados en el pirateo de programas y contenidos digitales, infringiendo la legislación sobre propiedad intelectual.
- **Creadores de virus y programas dañinos:** Se trata de expertos informáticos que pretenden demostrar sus conocimientos construyendo virus y otros programas dañinos, que distribuyen hoy en día a través de Internet para conseguir una propagación exponencial y alcanzar así una mayor notoriedad. En los últimos años la intención de estos creadores ha empezado a ser cada vez más delictiva, pues crean programas dañinos que roban información sensible de sus víctimas para posteriormente usarlos en estafas y operaciones fraudulentas.
- **Lammers (wannabes): Script-kiddies o Click-kiddies:** Los lammers, también conocidos por script kiddies o click kiddies, son aquellas personas que han obtenido determinados programas o herramientas para realizar ataques informáticos (descargándolos generalmente desde algún servidor de Internet) y que los utilizan sin tener conocimientos técnicos de cómo funcionan. A pesar de sus limitados conocimientos, son los responsables de la mayoría de los ataques que se producen en la actualidad. La abundancia de documentación técnica y de herramientas informáticas que pueden descargarse de Internet y ser utilizadas por personas sin conocimientos técnicos hace que este tipo de atacantes sean muy numerosos.
- **Amenazas del personal interno:** También debemos tener en cuenta el papel desempeñado por algunos empleados en muchos de los ataques e incidentes de seguridad informática, ya sea de forma voluntaria o involuntaria. Así, podríamos considerar el papel de los empleados que actúan como “fisgones” en la red informática de su organización, los usuarios incautos o despistados, o los empleados descontentos o desleales que pretenden causar algún daño a la organización. Por este motivo, conviene reforzar la seguridad de las empresas tanto en relación con el personal interno (insiders) como con los usuarios externos del sistema informático (outsiders).
- **Ex empleados:** Los ex empleados pueden actuar contra su antigua empresa u organización por despecho o venganza, accediendo en algunos casos a través de cuentas de usuario que todavía no han sido canceladas en los equipos y servidores de la organización. También pueden provocar la activación de “bombas lógicas” para causar determinados daños en el sistema informático (eliminación de ficheros, envío de información confidencial a terceros...) como venganza tras un despido.
- **Intrusos remunerados:** Los intrusos remunerados son expertos informáticos contratados por un tercero para la sustracción de información confidencial, llevar a cabo sabotajes informáticos contra una determinada organización, etcétera.
## Ataques informáticos
 Los ataques contra redes de ordenadores y sistemas informáticos suelen constar de las etapas o fases que se presentan a continuación:
 
- Descubrimiento y exploración del sistema informático.
- Búsqueda de vulnerabilidades en el sistema.
- Explotación de las vulnerabilidades detectadas.
- Corrupción o compromiso del sistema: modificación de programas y ficheros del sistema para dejar instaladas determinadas puertas traseras o troyanos; creación de nuevas cuentas con privilegios administrativos que faciliten el posterior acceso del atacante al sistema afectado, ...
- Eliminación de las pruebas que puedan revelar el ataque y el compromiso del sistema: eliminación o modificación de los registros de actividad del equipo (logs); modificación de los programas que se encargan de monitorizar la actividad del sistema, ....
 
Para poder llevar a cabo un ataque informático los intrusos deben disponer de los medios técnicos, los conocimientos y las herramientas adecuadas, deben contar con una determinada motivación o finalidad, y se tiene que dar además una determinada oportunidad que facilite el desarrollo del ataque (como podría ser el caso de un fallo en la seguridad del sistema informático elegido).
### Tipos de ataques informáticos
En una clasificación general, los principales tipos de ataques informáticos que existirían serían los siguientes:
 
- **Malware:**
El término Malware se refiere de forma genérica a cualquier software malicioso que tiene por objetivo infiltrarse en un sistema para dañarlo. Aunque se parece a lo que comúnmente se le conoce como virus, el virus es un tipo de malware. Igualmente existen otros como los gusanos, troyanos, etc.
 
- **Virus:**
El virus es un código que infecta los archivos del sistema mediante un código maligno, pero para que esto ocurra necesita que nosotros, como usuarios, lo ejecutemos. Una vez que se ejecuta, se disemina por todo nuestro sistema a donde nuestro equipo o cuenta de usuario tenga acceso, desde dispositivos hardware hasta unidades virtuales o ubicaciones remotas en una red.
 
- **Gusanos:**
Un gusano es un programa que, una vez infectado el equipo, realiza copias de sí mismo y las difunde por las red. A diferencia del virus, no necesita nuestra intervención, ni de un medio de respaldo, ya que pueden transmitirse utilizando las redes o el correo electrónico. Son difíciles de detectar, pues al tener como objetivo el difundirse e infectar a otros equipos, no afectan al funcionamiento normal del sistema.
Su uso principal es el de la creación de botnets, que son granjas de equipos zombies utilizados para ejecutar acciones de forma remota como por ejemplo un ataque DDoS a otro sistema.
 
- **Troyanos:**
Son similares a virus, pero no completamente iguales. Mientras que el virus es destructivo por sí mismo, el troyano lo que busca es abrir una puerta trasera para favorecer la entrada de otros programas maliciosos.
Su nombre es alusivo al “Caballo de Troya” ya que su misión es precisamente, pasar desapercibido e ingresar a los sistemas sin que sea detectado como una amenaza potencial. No se propagan a sí mismos y suelen estar integrados en archivos ejecutables aparentemente inofensivos.
 
- **Spyware:**
Un spyware es un programa espía, cuyo objetivo principal es obtener información. Su trabajo suele ser también silencioso, sin dar muestras de su funcionamiento, para que puedan recolectar información sobre nuestro equipo con total tranquilidad, e incluso instalar otros programas sin que nos demos cuenta de ello.
 
- **AdWare:**
La función principal del adware es la de mostrar publicidad. Aunque su intención no es la de dañar equipos, es considerado por algunos una clase de spyware, ya que puede llegar a recopilar y transmitir datos para estudiar el comportamiento de los usuarios y orientar mejor el tipo de publicidad.
 
- **Ransomware:**
Este es uno de los más sofisticados y modernos malwares ya que lo que hace es secuestrar datos (encriptándolos) y pedir un rescate por ellos. Normalmente, se solicita una transferencia en bitcoins, la moneda digital, para evitar el rastreo y localización. Este tipo de ciberataque va en aumento y es uno de los más temidos en la Actualidad.
 
- **Phishing:**
El phishing no es un software, se trata más bien de diversas técnicas de suplantación de identidad para obtener datos privados de las víctimas, como por ejemplo las contraseñas o datos de seguridad bancarios.
Los medios más utilizados son el correo electrónico, mensajería o llamadas telefónicas, se hacen pasar por alguna entidad u organización conocida, solicitando datos confidenciales, para posteriormente utilizar esos datos en beneficio propio.
 
## Bibliografía
- *Seguridad informática Hacking Ético - Conocer el ataque para una mejor defensa.* (2015) (3a edición). Barcelona: Ediciones ENI.
- Gómez Vieites, A. (2014) . *Seguridad en equipos informáticos* . Madrid: RA-MA Editorial.
