# PLAN DE SEGURIDAD Y ALTA DISPONIBILIDAD: SOLUCIONES TECNOLÓGICAS "TECH-REACH S.A."
## 1. Descripción del escenario (Contexto)
**Tech-Reach S.A.** es una empresa dedicada al desarrollo de software y consultoría IT con una plantilla de **45 empleados**. Su operatividad depende íntegramente de la disponibilidad de sus servicios alojados en el CPD local.

Al ser una empresa de software, la disponibilidad de los sistemas es clave para la continuidad de negocio así como para mantener su reputación ya que un error en el sistema o una pérdida de datos detendría la producción de forma inmediata.
### Servicios Críticos:
- **Servidor de Bases de Datos:** Contiene el código fuente de clientes y bases de datos de producción. Un fallo aquí detendría el desarrollo y la facturación.
	
- **Servidor de Archivos:** Repositorio de documentación técnica, contratos y activos digitales.
	
- **Infraestructura de Red:** Firewall y switches que permiten la conexión segura VPN para empleados en remoto y comunicación interna.

- **Suministro Eléctrico:** Crítico tanto para el CPD como para los puestos de trabajo de los desarrolladores.
## 2. Seguridad Física del CPD
### Ubicación de la sala de servidores
![000%20Assets/P1%20-%20Diseño%20de%20un%20plan%20básico%20de%20seguridad%20física%20y%20seguridad%20pasiva%20para%20una%20empresa/SyAD](000%20Assets/P1%20-%20Diseño%20de%20un%20plan%20básico%20de%20seguridad%20física%20y%20seguridad%20pasiva%20para%20una%20empresa/SyAD.png)

Las instalaciones de la empresa Tech-Reach se encuentran en el Parque Tecnológico de Leganés en Madrid, encontrándose lejos de zonas industriales y subestaciones de alta tensión que podrían suponer un riesgo.

La empresa ocupa un edificio de tres plantas, lo que permite una separación física de departamentos y una gestión de riesgos ambientales optimizada. A continuación se muestra la distribución de departamentos por planta:
#### Distribución de Seguridad por Niveles
- **Planta Baja:** Recepción, atención al cliente y hall de entrada.
- **Planta Primera:** Aquí se ubican las oficinas de desarrollo y, lo más importante, el **CPD**.
- **Planta Segunda:** Dirección General, Administración y Recursos Humanos.
- **Azotea:** Ubicación del **Grupo Electrógeno** y condensadoras de aire acondicionado.

La decisión de la ubicación del CPD se ha tomado tras el estudio de riesgos para el mismo, evitándose así:

- **Riesgos ambientales** tanto inundaciones (fugas de agua o lluvias torrenciales) en planta baja como filtraciones por tejado o calor excesivo por radiación solar en la última planta.
- **Riesgos internos**: La sala está lejos de cuadros eléctricos, tuberías y depósitos de agua y zonas de cafetería para evitar interferencias y fugas.
- **Control de Accesos**: Al no estar en la planta de paso (baja), es más fácil controlar que solo el personal autorizado con **Doble Factor de Autenticación** acceda a la sala.
### Control de accesos físicos
Se ha implementado un sistema de seguridad por capas para asegurar que solo el personal autorizado interactúe con los activos críticos de la empresa.

El edificio se divide en áreas con niveles de restricción progresivos para mitigar riesgos de intrusión y sabotaje:

1. **Zona Pública (planta baja):** Hall de entrada y recepción con registro de visitantes externos.
2. **Zona de Personal (plantas 1 y 2):** Espacios destinados a oficinas generales y desarrollo.
3. **Zona de Acceso Restringido:** CPD (planta 1), sótano y azotea.

A continuación desarrollamos cada una de estas zonas:
#### 1. Zona de Acceso Público (Planta Baja)
En la entrada del edificio existe una recepción atendida que lleva un control detallado de toda persona ajena a la compañía, registrando su identidad y motivo de la visita.
#### 2. Zona de Acceso al Personal (Oficinas - Planta 1 y 2)
Separada de la zona pública por puertas con apertura mediante tarjeta RFID nominal. De esta forma cada empleado accede únicamente a las zonas necesarias para su puesto de trabajo aplicando así el principio del mínimo privilegio.
#### 3. Zona de Acceso Restringido (CPD e Infraestructura Crítica)
Estas zonas comprenden los puntos únicos de fallo del sistema donde el acceso es extremadamente limitado. De modo que estas salas disponen de puertas de seguridad donde el acceso requiere la combinación de tarjeta RFID y código PIN.

- **Ubicación Principal (CPD - Planta 1):** Alberga los servidores de bases de datos, archivos y equipos de red.

- **Infraestructura de Soporte (Sótano y Azotea):** 
	- **Sótano:** Aloja el cuarto de acometidas (entrada de fibra óptica y red eléctrica general) y depósitos.
    - **Azotea:** Ubicación del **Grupo Electrógeno** diésel, protegido por un vallado perimetral con acceso restringido.
#### 4. Vigilancia y Supervisión
- **CCTV 24/7:** Todo el edificio cuenta con videovigilancia en puntos estratégicos, incluyendo los accesos a las zonas restringidas y el interior del CPD (frontal y trasera de racks).

- **Acompañamiento:** Cualquier técnico externo debe estar bajo supervisión permanente de un responsable de IT y haber firmado previamente un acuerdo de confidencialidad.

- **Registro de Logs:** Cada entrada y salida en zonas críticas genera un registro automático con los datos del usuario y la hora exacta.   
### Infraestructura del CPD
En este apartado se describe el diseño físico y el equipamiento técnico necesario para soportar los servicios críticos de la empresa TECH-REACH. El CPD se ubica en la **planta primera** del edificio para garantizar la protección contra riesgos ambientales y optimizar la distribución de cableado.
#### 1. Diseño y Distribución Física
La sala técnica ha sido diseñada bajo criterios de alta disponibilidad, utilizando una configuración de **pasillos fríos y pasillos calientes** para optimizar la eficiencia de la climatización.

- **Cerramientos, canalización y cableado:** Paredes con resistencia al fuego RF-120 y suelo técnico con baldosas registrables a 40 cm de altura para la canalización de cableado y flujo de aire. Durante la canalización se separa el cableado eléctrico del de datos.

- **Armarios Rack:** Aunque por espacio físico todos los equipos cabrían en uno solo se instalan **dos Racks de 42U (19")** para garantizar **redundancia física** y **gestión térmica**. La distribución lógica es la siguiente:
	- **Rack A: Nodo de Producción y Comunicaciones**
		- **Equipos:** Servidor de BBDD, Switch, Firewall, Router y KVM (Monitor).
		- **Función:** Es el rack "vivo", el que da el servicio a los clientes y empleados en tiempo real.
	- **Rack B: Nodo de Almacenamiento y Backup**
		- **Equipos:** Servidor de Archivos, Servidor de Backups y la unidad NAS.
		- **Función:** Es el rack de "datos pasivos" y seguridad. Al separarlo, si ocurre un fallo eléctrico grave o un cortocircuito en el Rack A que provoque un pequeño incendio local, los datos del Rack B tienen más probabilidades de sobrevivir.
#### 2. Inventario de Equipamiento Técnico
A continuación, se detalla el hardware activo que compone la infraestructura de Tech-Reach S.A. y su consumo eléctrico asociado para el cálculo de los sistemas de respaldo (o redundancia) para garantizar la continuidad de negocio en tres niveles:
- Respaldo de Energía (Continuidad Eléctrica)
- Respaldo de Datos (Copias de Seguridad)
- Respaldo de Hardware (Redundancia)

| Cant. | Equipo               | Función Técnica                              | Voltaje | Consumo (W) |
|-------|----------------------|----------------------------------------------|---------|-------------|
| 1     | Servidor BBDD        | Gestión de bases de datos y proyectos.       | 230V    | 500 W       |
| 1     | Servidor de Archivos | Almacenamiento operativo de documentos.      | 230V    | 350 W       |
| 1     | Servidor de Backups  | Repositorio para copias de seguridad.        | 230V    | 350 W       |
| 1     | NAS                  | Almacenamiento de red secundario.            | 230V    | 100 W       |
| 1     | Switch               | Conectividad de red y alimentación PoE.      | 230V    | 150 W       |
| 1     | Firewall             | Seguridad perimetral y túneles VPN.          | 230V    | 40 W        |
| 1     | Monitor (KVM)        | Gestión y monitorización en el rack.         | 230V    | 30 W        |
| 1     | Router               | Gateway de acceso a Internet.                | 230V    | 50 W        |
| 2     | Ventilación Rack     | Sistemas de extracción de aire (1 por rack). | 230V    | 50 W        |
| 2     | PDU                  | Unidades de distribución de energía.         | 230V    | 10 W        |
### Protección Eléctrica
La instalación eléctrica del CPD y sus activos de soporte se divide en dos niveles de protección:
- Sistema de Alimentación Ininterrumpida (SAI/UPS)
- Grupo Electrógeno (Generador)
#### 1. Sistema de Alimentación Ininterrumpida (SAI/UPS)
Se han seleccionado **2 unidades SAI de tipo Online / Doble conversión 3000VA (3kVA)** para trabajar en paralelo o dividiendo la carga, asegurando que el sistema opere de forma holgada y con alta disponibilidad al tener redundancia (N+1).

- **Funcionamiento**: Este sistema regenera completamente la corriente eléctrica sin delay, eliminando ruidos, picos de tensión y variaciones de frecuencia de forma constante.

- **Configuración Redundante con Alimentación Cruzada**: Siguiendo el modelo de alta disponibilidad, se instalan **dos unidades SAI Online de 3.000 VA físicamente independientes** donde los equipos con fuente de alimentación redundante se conectan simultáneamente a ambos SAIs. De esta forma, la **Unidad SAI 1** y la **Unidad SAI 2** no actúan como compartimentos estancos, sino como un sistema de respaldo mutuo: ante el fallo total de uno de los SAIs, la infraestructura completa de Tech-Reach S.A. permanece operativa.

- **Autonomía**: Se garantiza un tiempo de respaldo de entre **20 y 30 minutos** a plena carga. Este margen es suficiente para que el generador externo entre en funcionamiento o para realizar un apagado ordenado de los sistemas si fuera necesario.

- **Ubicación**: Los SAI se encuentran en una sala separada en el propio CPD, para proteger los servidores y equipos de red de posibles riesgos generados por ellos. La sala cuenta con ventilación propia, y puerta ignífuga.
##### Cálculos para el Dimensionamiento y análisis de un SAI
![000%20Assets/P1%20-%20Diseño%20de%20un%20plan%20básico%20de%20seguridad%20física%20y%20seguridad%20pasiva%20para%20una%20empresa/SyAD-1](000%20Assets/P1%20-%20Diseño%20de%20un%20plan%20básico%20de%20seguridad%20física%20y%20seguridad%20pasiva%20para%20una%20empresa/SyAD-1.png)

```math
# Suma de potencia real para calcular el consumo de vatios total
consumo_total = 500 + 350 + 350 + 100 + 150 + 40 + 30 + 50 + 50 + 10

# Cálculo de potencia necesaria añadiendo un 20% de margen de seguridad para evitar que el sai trabaje al limite de su capacidad
potencia_necesaria = consumo_total * 1.20

# coversion a VA para elegir el SAI adecuado
potencia_minima = potencia_necesaria * 1.25
```

#### 2. Grupo Electrógeno (Generador)
Para cortes de suministro de larga duración, se dispone de un generador diésel ubicado en la **Azotea** del edificio.

- **Activación Autónoma**: El sistema detecta automáticamente la ausencia de red eléctrica y se activa de forma independiente, asumiendo la carga total del CPD en menos de un minuto.

- **Alcance del Servicio**: El generador da servicio exclusivamente a la infraestructura crítica: sistemas de climatización, servidores y recarga de los propios SAIs.

- **Seguridad Física**: Se encuentra en una zona de **Acceso Restringido** con vallado perimetral para evitar sabotajes en el suministro de combustible o el cableado.
### Protección contra incendios
Para proteger el CPD de **Tech-Reach S.A.**, no podemos usar agua ni extintores de polvo convencionales, ya que destruirían los circuitos de los servidores antes que el propio fuego. 

- **Detección Precoz:** Se han instalado **detectores de humo ópticos** y **sistemas de aspiración de alta sensibilidad (tipo VESDA)** para identificar partículas de humo en una fase temprana del riesgo de incendio.

- **Extinción:** Sistema de inundación mediante **Gas Novec 1230**. A diferencia del agua o el CO2 extremo, este agente químico extingue el fuego por enfriamiento sin dañar los circuitos electrónicos y sin dejar residuos, permitiendo reanudar la marcha tras ventilar la sala.

- **Protocolo de Actuación ante incendios:** En todo el edificio se encuentra la señalización pertinente y plano de evacuación, se realizan simulacros de manera periódica y se asegura la entrega, lectura y comprensión del plan de actuación por parte de todos los empleados.
### Condiciones ambientales
En el apartado de [Diseño y Distribución Física](#1-diseño-y-distribución-física) de la [Infraestructura del CPD](#Infraestructura-del-CPD), se menciona el uso de pasillos fríos y calientes (**sistemas HVAC**) para garantizar el rendimiento óptimo del hardware y aumentar su vida útil. Para mantener una temperatura “ideal” y constante entre 18 y 27Cº para cumplir con la recomendaciones de la ASHRAE, es necesario el uso de sensores para medir:
- Temperatura y Humedad
- Fugas de agua
- Calidad del aire.
### Gestión de personal y visitantes
Existen diferentes protocolos de actuación para asegurar la integridad de las instalaciones y evitar accesos no autorizados que puedan poner en peligro los activos de la compañía.
#### Control de Empleados (Personal Interno)
- **Identificación RFID:** Cada empleado dispone de una tarjeta nominal e intransferible que abre las puertas de su zona de trabajo (Planta 1 o 2).
- **Registro de Jornada:** El sistema de acceso sirve también como registro de entrada y salida, permitiendo saber en tiempo real quién está en el edificio en caso de emergencia o evacuación.
- **Niveles de Privilegio:** Un empleado de Administración no tiene acceso permitido al CPD; su tarjeta solo desbloqueará las puertas de las oficinas generales
#### Visitantes y Externos
Cualquier persona ajena a la empresa (clientes, mensajería, candidatos) debe seguir este flujo obligatorio en la **Planta Baja**:
- **Recepción y Registro:** El personal de seguridad solicita el DNI/NIE y registra la hora de entrada, el motivo de la visita y la persona de contacto interna.
- **Acreditación Temporal:** Se entrega un distintivo de "Visitante" de color llamativo que debe portar de forma visible.
- **Acompañamiento:** Un visitante nunca puede circular solo por las plantas 1 o 2. Debe ser recogido en el hall por un empleado de Tech-Reach y permanecer bajo su supervisión hasta que abandone el edificio.
#### Acceso de Personal Técnico y Mantenimiento
Es el caso más sensible, ya que suelen necesitar entrar en la **Zona de Acceso Restringido** (CPD, Sótano o Azotea):
- **Autorización Previa:** El servicio técnico debe estar programado y autorizado por el responsable de IT.
- **Acuerdo de Confidencialidad (NDA):** Antes de entrar al CPD, deben firmar un documento donde se comprometen a no manipular ni fotografiar información sensible.
- **Supervisión Continua:** Durante toda la intervención en el rack o el grupo electrógeno, un técnico de la casa (perfil ASIR) debe estar presente para supervisar las tareas.
#### Datos almacenados sobre visitantes:
- Nombre y apellidos, DNI y empresa en la que trabaja.
- Motivo de la visita.
- Empleado de la compañía que supervisa al visitante.
- Hora de entrada y de salida
## 3. Seguridad Pasiva y Almacenamiento
### Tipo de almacenamiento
Para Tech-Reach, hemos implementado una solución de **Almacenamiento Híbrido**. Esta combinación permite velocidad local y seguridad geográfica.

- **Servidor de Archivos (Almacenamiento Local):** Es el almacenamiento **primario y principal**. Se utiliza con Windows Server para gestionar el acceso diario de los 45 empleados ya que proporciona la latencia más baja (velocidad instantánea) para trabajar con documentos en la red local y permite un control total sobre los permisos y la privacidad de los datos.
        
- **Nube (AWS S3 - Almacenamiento Remoto):** Es el almacenamiento de **respaldo externo**. De esta forma se cumple con la normativa de seguridad de datos al tener una copia fuera de las instalaciones físicas (Off-site). Si el edificio de Leganés sufriera un desastre (incendio o inundación), los datos de la empresa estarían a salvo en la infraestructura global de Amazon.
### Sistema RAID
Para garantizar el equilibrio entre rendimiento, capacidad y seguridad, se ha diseñado una arquitectura de almacenamiento diferenciada para los tres servidores principales:
#### 1. Servidor de Base de Datos - RAID 10 (Striping de Espejos)
- Se requiere rendimiento y velocidad de escritura y a su vez seguridad de los datos para que las consultas a las bases de datos sean instantáneas para los 45 empleados y ofrece una recuperación inmediata ante el fallo de un disco, sin afectar la velocidad del servicio.
#### 2. Servidor de Archivos - RAID 5 (Paridad Distribuida) 
En este servidor prima la **capacidad neta disponible** para almacenar historiales, documentos de proyectos y archivos multimedia. El RAID 5 es la opción más eficiente aquí, ya que permite aprovechar la mayor parte del espacio de los discos manteniendo la seguridad: si un disco falla, la paridad distribuida permite reconstruir los datos sin pérdida de información.
#### 3. Servidor de Copias de Seguridad - RAID 6 (Doble Paridad)**
Este es el sistema de máxima criticidad para la integridad de los datos. Se elige RAID 6 porque permite que **fallen hasta dos discos simultáneamente** sin que las copias de seguridad se vean afectadas. Es el "seguro de vida" de la empresa ante fallos múltiples durante procesos de reconstrucción de datos.

### Diferencia entre RAID y Copias de Seguridad
El RAID garantiza **disponibilidad**, el Backup garantiza **recuperación**.

- **Ejemplo:** Si un empleado borra accidentalmente una carpeta, el RAID replicará ese borrado en todos los discos al instante (la información se pierde). Sin embargo, la **copia de seguridad** permitirá "viajar en el tiempo" al día anterior y restaurar dicha carpeta.
## 4. Plan de Copias de Seguridad

El plan de copias de seguridad sigue la estrategia 3-2-1: Tres copias, en Dos soportes diferentes y Una de ellas se encuentra en una ubicación diferente.

Las dos ubicaciones son el Servidor de Copias de Seguridad del CPD y un servidor de copias de seguridad en la nube.
#### Cronograma de copias:
- **Copia Completa (Full):** Se realiza cada dos semanas (Domingo noche).
- **Copia Incremental:** Solo guarda los cambios realizados desde la última copia. Al ser incrementales, son muy ligeras y permiten ejecutarlas varias veces al día sin afectar al rendimiento de la red. Se realiza cada 8 horas teniendo en cuenta el RPO.
#### Medidas de Protección y Verificación
Todas las copias se cifrarán mediante **AES-256 bits** para evitar que, en caso de robo físico de los soportes, la información sea legible. El acceso al servidor de backups estará restringido a una sola cuenta de administrador con 2FA.    
## 5. Recuperación ante Incidentes
#### Nivel 1: Borrado accidental de un archivo
1. El administrador accede al software de gestión de backups en el **Servidor de Copias de Seguridad**. 
2. Se selecciona el punto de restauración más cercano (copia incremental). 
3. Se realiza una **restauración granular** (solo el archivo afectado) directamente al Servidor de Archivos a través de la red local.
    
**Tiempo estimado (RTO):** 5-10 minutos.
#### Nivel 2: Fallo grave de un servidor (Hardware)
1. Si el fallo es solo de discos, el RAID ya debería haberlo absorbido. Si el servidor muere por completo, se procede a levantar una instancia del servidor afectado en el Host de Virtualización para garantizar la continuidad.
2. Una vez reparado el hardware o sustituido el servidor, se restaura la última imagen completa más las incrementales desde el Servidor de Backups local.

- **Tiempo estimado (RTO):** 1 a 4 horas.
#### Nivel 3: Incidente crítico (Incendio, Ransomware o Pérdida Total)
1. **Ransomware** 
	- **Aislamiento**: Se desconecta la red local para evitar que el ransomware llegue a la nube. No pagar.
	- **Evaluación** para identificar el alcance y el vector de entrada
	- **Erradicación**: formateos a bajo nivel de los discos afectados.
	- **Recuperación**: restauración limpia desde la copia de seguridad, previa verificación de no contener la carga viral o descargar las copias de seguridad desde **AWS S3**.
	- **Comunicación** a la Agencia Española de Protección de Datos (AEPD) en un periodo máximo de 72h y activación del comité de seguridad para notificación a los posibles afectados.

2. **CPD inaccesible (incendio)**
	- Si la oficina es inhabitable, se pueden levantar los servidores directamente en instancias de **Amazon EC2** para que los 45 empleados trabajen en remoto mediante VPN mientras se reconstruye el CPD físico.
