# Día Bonus — Guía #StopRansomware (CISA · FBI · NSA · MS-ISAC)

**Basado en:** #StopRansomware Guide — CISA, FBI, NSA, MS-ISAC (septiembre 2023)
**Fuente oficial:** https://www.cisa.gov/stopransomware/ransomware-guide
**Audiencia:** IT, ingeniería, calidad, administración — industria manufacturera
**Duración sugerida:** 4 horas

---

## Contexto de la guía

El ransomware es malware diseñado para cifrar archivos en un dispositivo, dejándolos inutilizables. Los actores maliciosos exigen rescate a cambio del descifrado. Con el tiempo han añadido la **exfiltración de datos** como palanca adicional de presión — amenazando con publicar la información si no se paga. Esta táctica combinada se conoce como **"doble extorsión"**.

Esta guía fue desarrollada por la **Joint Ransomware Task Force** y contiene dos partes:

| Parte | Contenido |
|-------|-----------|
| **Parte 1** | Mejores prácticas de preparación, prevención y mitigación |
| **Parte 2** | Checklist de respuesta ante un incidente activo |

Las recomendaciones están mapeadas a los **Cybersecurity Performance Goals (CPGs)** de CISA/NIST.

---

## Bloque 1 — Parte 1: Preparación y prevención por vector de ataque

**Duración:** 1 hora

---

### Preparación ante ransomware y extorsión de datos

Antes de que ocurra un ataque, CISA recomienda estos pasos fundamentales:

#### Backups y recuperación

- [ ] Mantener **backups offline cifrados** de datos críticos y probar disponibilidad e integridad regularmente en escenario de recuperación ante desastres `[CPG 2.R]`
  - Muchas variantes de ransomware buscan y eliminan o cifran backups accesibles para hacer imposible la restauración sin pagar
- [ ] Mantener **"golden images"** actualizadas de sistemas críticos: plantillas con SO y software preconfigurados que pueden desplegarse rápidamente para reconstruir un sistema `[CPG 2.O]`
- [ ] Usar **Infrastructure as Code (IaC)** para desplegar y actualizar recursos en nube; guardar copias offline de los archivos de plantilla
- [ ] Considerar solución **multi-nube** para evitar vendor lock-in en backups cloud-a-cloud
- [ ] Algunos proveedores cloud ofrecen **almacenamiento inmutable** (Object Lock en S3, Azure Blob) — usar con precaución por posibles costos de mala configuración

#### Plan de Respuesta a Incidentes

- [ ] Crear, mantener y ejercitar regularmente un **Plan de Respuesta a Incidentes (IRP)** básico con procedimientos de notificación para ransomware y brechas de datos `[CPG 2.S]`
- [ ] Mantener copia impresa y versión offline del plan
- [ ] Asegurar que el IRP sea revisado y aprobado por el CEO (o equivalente) por escrito
- [ ] Incluir procedimientos de comunicación y plantillas de declaraciones ante incidentes
- [ ] Verificar que los procedimientos de notificación de brecha cumplan con las leyes aplicables (en México: **LFPDPPP**, notificación a **INAI** en 72 horas)

#### Zero Trust Architecture

- [ ] Implementar **arquitectura Zero Trust (ZTA)** para prevenir acceso no autorizado a datos y servicios
- [ ] ZTA asume que la red está comprometida y aplica el principio de mínimo privilegio por cada solicitud de acceso
- [ ] Hacer el control de acceso lo más granular posible

---

### Vector 1: Vulnerabilidades y malas configuraciones expuestas a internet

| Riesgo | Control CISA recomendado |
|--------|--------------------------|
| RDP expuesto sin protección | No exponer RDP a internet; si es necesario, aplicar MFA y limitar por IP `[CPG 2.W]` |
| Software sin parchear | Priorizar parcheo de servidores expuestos a internet, especialmente CVEs conocidos explotados |
| Puertos y protocolos innecesarios | Deshabilitar todo lo que no se use en activos expuestos `[CPG 2.X]` |
| Configuración en nube incorrecta | Usar IaC para codificar configuración; verificar deriva de configuración regularmente |

#### Hardening de RDP
- Auditar la red para identificar sistemas con RDP activo
- Cerrar puertos RDP no utilizados
- Aplicar bloqueo de cuenta tras N intentos fallidos
- Implementar **MFA obligatorio** en todo acceso RDP
- Registrar y revisar intentos de login en RDP

#### Hardening de SMB (Server Message Block)
- Deshabilitar **SMBv1** completamente; migrar a **SMBv3**
- Requerir **SMB 3.1.1** (incluye protecciones de integridad pre-autenticación, cifrado AES y firma criptográfica)
- Bloquear SMB en el perímetro: TCP 445, 137, 138, 139 bloqueados hacia/desde internet
- Limitar tráfico SMB interno a solo sistemas que lo requieren
- Configurar **SMB Encryption** o al mínimo **SMB Signing** en todos los sistemas
- Habilitar SMB sobre QUIC donde sea posible (Windows 11 / Server 2022)
- Monitorear y registrar tráfico SMB para detectar comportamientos anómalos `[CPG 2.T]`

#### VPN y acceso remoto
- Actualizar VPNs con últimos parches de seguridad
- Implementar MFA en **todas** las conexiones VPN; si no es posible, requerir contraseñas de mínimo 15 caracteres
- Referencia: CISA Advisory: Enterprise VPN Security

---

### Vector 2: Credenciales comprometidas

- [ ] Implementar **MFA resistente a phishing** para todos los servicios, especialmente correo, VPNs y sistemas críticos `[CPG 2.H]`
  - Considerar MFA sin contraseña (passwordless): huella dactilar, reconocimiento facial, PIN de dispositivo, llave criptográfica
- [ ] Cambiar **nombres de usuario y contraseñas predeterminadas** `[CPG 2.A]`
- [ ] **No usar cuentas root** para operaciones diarias — crear usuarios, grupos y roles para tareas específicas
- [ ] Política de contraseñas: mínimo **15 caracteres únicos** `[CPG 2.B]` `[CPG 2.C]`
- [ ] Gestores de contraseñas: usar y proteger con MFA habilitado
- [ ] Políticas de **bloqueo de cuenta** tras cierto número de intentos fallidos; registrar y monitorear intentos de fuerza bruta `[CPG 2.G]`
- [ ] Almacenar contraseñas con **hashing robusto**; deshabilitar guardado de contraseñas en navegadores vía GPO
- [ ] Implementar **LAPS** (Local Administrator Password Solution) en sistemas anteriores a Windows Server 2019 / Windows 10
- [ ] Proteger contra volcado de **LSASS**:
  - Implementar regla ASR (Attack Surface Reduction) para LSASS
  - Habilitar **Credential Guard** en Windows 10 / Server 2016
- [ ] Separar **cuentas de administrador** de cuentas de uso diario `[CPG 2.E]`
- [ ] Auditar cuentas de usuario y administrador trimestralmente; revisar accesos de terceros y MSPs
- [ ] Suscribirse a servicios de **monitoreo de credenciales** en dark web

---

### Vector 3: Phishing

- [ ] Programa de **concientización y capacitación** con instrucciones sobre cómo identificar y reportar actividad sospechosa `[CPG 2.I]`
- [ ] Marcar correos externos con etiqueta visible en el cliente de correo
- [ ] Filtros en el **gateway de correo** para bloquear IPs maliciosas conocidas y asuntos sospechosos `[CPG 2.M]`
- [ ] Habilitar filtros de **adjuntos comunes**: `.exe`, `.bat`, `.js`, `.vbs`, `.ps1`, `.msi`, `.lnk`, `.iso`
  - Revisar lista de tipos de archivo al menos semestralmente — agregar vectores emergentes (ej. OneNote `.one` con malware embebido)
  - El malware frecuentemente se comprime en archivos protegidos con contraseña para evadir filtros
- [ ] Implementar **DMARC**, **DKIM** y **SPF** en el dominio corporativo `[CPG 2.M]`
- [ ] **Deshabilitar macros de Office** en archivos transmitidos por correo; en versiones recientes de Office las macros VBA de internet están bloqueadas por defecto `[CPG 2.N]`
- [ ] Deshabilitar **Windows Script Host (WSH)**

---

### Vector 4: Malware precursor

Muchas infecciones de ransomware son consecuencia de una **infección previa no resuelta** con malware tipo dropper:

| Malware precursor | Descripción |
|------------------|-------------|
| **QakBot** | Troyano bancario, vende acceso a redes comprometidas |
| **Bumblebee** | Loader distribuido vía phishing, precursor de Conti/LockBit |
| **Emotet** | Botnet modular; fue desmantelado en 2021 pero resurgió |
| **Dridex** | Troyano financiero, precursor de BitPaymer/DoppelPaymer |

> Los operadores de estos malware frecuentemente venden acceso a redes a grupos de ransomware. Primero exfiltran datos, luego ransoMean la red para mayor presión.

- [ ] Actualizaciones automáticas de **antivirus/anti-malware** y firmas; solución centralizada `[CPG]`
- [ ] **Application allowlisting** y/o soluciones **EDR** en todos los activos
  - Windows: habilitar **WDAC** (Windows Defender Application Control) y/o **AppLocker**
  - WDAC tiene desarrollo continuo; AppLocker solo recibe fixes de seguridad
  - Considerar EDR para recursos en nube
- [ ] Implementar **IDS** para detectar actividad C2 y movimiento lateral previo al despliegue de ransomware
- [ ] Usar **Sysmon 14+** con opción `FileBlockExecutable` para bloquear creación de ejecutables maliciosos

---

### Vector 5: Ingeniería social avanzada

- [ ] Capacitación para reconocer sitios web ilegítimos y resultados de búsqueda manipulados
- [ ] Repetir capacitación regularmente — no solo en el onboarding
- [ ] Implementar **DNS Protector** (Protective DNS): bloquea dominios maliciosos a nivel DNS antes de que el usuario los visite
  - CISA ofrece servicio gratuito **MDBR** para organizaciones SLTT
  - Referencia: NSA/CISA "Selecting a Protective DNS Service"
- [ ] Considerar **navegadores en sandbox** para aislar la máquina host de código malicioso durante la navegación

---

### Vector 6: Terceros y proveedores de servicios (MSPs)

Los MSPs han sido vector de infección para ransomware que impactó a múltiples organizaciones clientes simultáneamente `[CPG 1.I]`.

- [ ] Evaluar las prácticas de higiene cibernética de terceros y MSPs con acceso a tu red
- [ ] Si un tercero gestiona backups, verificar que sigue las mejores prácticas de esta guía; formalizar requisitos de seguridad en **contrato**
- [ ] Principio de **mínimo privilegio** para accesos de terceros — solo dispositivos y servidores dentro de su rol
- [ ] Usar **Service Control Policies (SCP)** en entornos cloud para restringir qué pueden hacer usuarios o roles de terceros (ej. impedir borrar logs, modificar VPCs, cambiar configuración de logging)

---

### Mejores prácticas generales y hardening

#### Gestión de activos `[CPG 1.A]`
- Inventariar activos lógicos (datos, software) y físicos (hardware)
- Identificar qué sistemas son más críticos para salud, seguridad, ingresos u operaciones críticas
- Aplicar controles más robustos en activos críticos
- Almacenar documentación de activos con copias offline y físicas

#### Principio de mínimo privilegio `[CPG 2.E]`
- Restringir permisos de instalación de software a usuarios
- Limitar acciones sobre recursos en nube
- Bloquear cuentas locales para acceso remoto mediante GPO
- Usar **Windows Defender Remote Credential Guard** y modo admin restringido para RDP

#### PowerShell
- Restringir uso de PowerShell solo a administradores que lo requieren, vía GPO
- Actualizar a **PowerShell 5.x o Core** más reciente; desinstalar versiones anteriores
- Habilitar **Module Logging**, **Script Block Logging** y **Transcription Logging**
- Retener logs de PowerShell al menos **180 días** con máximo tamaño de almacenamiento
- Deshabilitar PowerShell v2 (sin logging, sin protecciones modernas)

#### Domain Controllers (DCs)
- Usar versión más reciente de Windows Server soportada (recomendado: **Windows Server 2019+**)
- Parchear DCs regularmente; aplicar críticos tan pronto como sea posible
- Instalar software mínimo en DCs — cada agente puede ser vector de ejecución arbitraria
- Restringir acceso a DCs al grupo Administrators con cuentas dedicadas solo para admin
- No usar DCs para correo, navegación ni actividades de riesgo
- Configurar firewall de host en DCs para **bloquear acceso directo a internet**
- Implementar solución **PAM** en DCs para gestionar y monitorear acceso privilegiado
- Deshabilitar o limitar **NTLM/WDigest** — migrar a SAML, OIDC o Kerberos con AES-256
- Habilitar **Extended Protection for Authentication (EPA)**

#### Nube y entornos híbridos
- Revisar el **modelo de responsabilidad compartida** del proveedor cloud
- Activar logging en todos los recursos; configurar alertas para uso anómalo
- Habilitar **Object Lock / Delete Protection** en almacenamiento (object, database, file, block) para prevenir eliminación o sobreescritura
- Habilitar **versionado de objetos** para facilitar recuperación ante acciones maliciosas
- Usar **signed API requests** para acceso programático para verificar identidad del solicitante
- Referencia: CISA Advisory — Microsoft Office 365 Security Recommendations

#### Software RMM (Remote Monitoring and Management)
Los actores de ransomware usan herramientas RMM legítimas para mantener persistencia y evadir detección:
- Auditar herramientas RMM autorizadas en la red
- Revisar logs para detectar RMM ejecutado como **portable executable** (sin instalación)
- Requerir que RMM solo opere desde dentro de la red, vía VPN o VDI aprobados
- Bloquear conexiones entrantes/salientes en puertos comunes de RMM en el perímetro

#### Segmentación de red `[CPG 2.F]`
- Implementar ZTA y separar unidades de negocio, departamentos de IT, y **OT de IT**
- Desarrollar y mantener **diagrama de red** actualizado con sistemas, flujos de datos, topología, y conexiones de terceros `[CPG 2.P]`
- Guardar documentación de red offline y en copia física
- Monitorear tráfico este-oeste (lateral) con NetFlow o Zeek

#### Logging y monitoreo
- Retener y asegurar logs de dispositivos de red, hosts locales y servicios cloud
- Implementar **SIEM centralizado** para correlacionar logs de múltiples fuentes `[CPG 2.U]`
- Mantener logs de sistemas críticos por mínimo **un año** `[CPG 2.T]`
- Establecer **baseline de tráfico normal** y afinar detección de anomalías
- Considerar logging de transacciones de negocio para analítica de comportamiento

---

## Lab 1 — Evaluación de superficie de ataque real

**Plataforma:** CISA CSET (Cyber Security Evaluation Tool) + Shodan.io
**Acceso gratuito:** https://www.cisa.gov/resources-tools/services/cyber-security-evaluation-tool-cset
**Duración:** 1 hora

### Objetivo

Ejecutar la **Ransomware Readiness Assessment (RRA)** del CSET de CISA en el perfil de la planta y generar reporte de brechas.

### Pasos

**Parte A — CISA CSET Ransomware Readiness Assessment (35 min)**

1. Descargar e instalar CSET desde: https://github.com/cisagov/cset/releases
2. Crear nueva evaluación → seleccionar **"Ransomware Readiness Assessment (RRA)"**
3. Completar el cuestionario por niveles (Básico → Intermedio → Avanzado):
   - Nivel 1 — Prácticas básicas de higiene (backups, parcheo, MFA)
   - Nivel 2 — Controles intermedios (EDR, segmentación, logging)
   - Nivel 3 — Prácticas avanzadas (ZTA, threat hunting, IRP ejercitado)
4. Exportar reporte PDF con puntuación y brechas identificadas

**Parte B — Shodan para activos expuestos (15 min)**

```bash
# En Shodan.io buscar exposición del dominio/rango IP de la planta:
# org:"Nombre de la empresa"
# port:3389 country:MX
# port:445 country:MX
# hostname:"dominio-empresa.com"
```

5. Documentar cualquier activo identificado con RDP (3389) o SMB (445) expuesto
6. Verificar si aparece banner con versión de SO o software

**Tabla de hallazgos:**

| Activo encontrado | Puerto/Servicio | Versión expuesta | Riesgo | Acción inmediata |
|------------------|----------------|-----------------|--------|-----------------|
| | | | | |

**Resultado esperado:** RRA completada con identificación de al menos 2 brechas por nivel; tabla de activos expuestos llena.

---

## Lab 2 — Detección y análisis de indicadores de compromiso

**Plataforma:** Blue Team Labs Online + ID Ransomware
**Acceso gratuito:** https://blueteamlabs.online · https://id-ransomware.malwarehunterteam.com
**Duración:** 1 hora

### Objetivo

Ejecutar la fase de **Detección y Análisis** del checklist CISA usando herramientas reales de threat hunting.

### Indicadores que CISA recomienda buscar activamente

#### En entornos Windows corporativos:

| Indicador | Herramienta de detección | Por qué importa |
|-----------|------------------------|----------------|
| Cuentas AD nuevas o con privilegios escalados | AD Users & Computers / logs | Movimiento lateral post-compromiso |
| Logins VPN anómalos | Logs de VPN / SIEM | Punto de entrada más común |
| Uso de `bcdedit.exe`, `fsutil.exe deletejournal`, `vssadmin.exe`, `wbadmin.exe`, `wmic.exe shadowcopy` | Event ID 4688, Sysmon | Ransomware inhibe recuperación borrando shadow copies |
| Presencia de **Cobalt Strike** (procesos con nombres de procesos legítimos de Windows) | EDR / AV / Sysmon | Herramienta de pentesting usada masivamente por actores de ransomware |
| Software **RMM no autorizado** corriendo como portable executable | Sysmon / Process Monitor | Mecanismo de persistencia post-compromiso |
| Uso inesperado de PowerShell o PsTools | PowerShell logs / Event ID 4103, 4104 | Ejecución remota de malware |
| Volcado de credenciales AD / LSASS (`Mimikatz`, `NTDSutil.exe`) | Sysmon / EDR | Preparación para movimiento lateral masivo |
| Comunicaciones inesperadas endpoint-a-endpoint | NetFlow / Zeek | Movimiento lateral activo |
| Volumen anormal de datos salientes en cualquier puerto | NetFlow | Exfiltración de datos (doble extorsión) |
| Uso de `Rclone`, `Rsync`, FTP/SFTP hacia IPs externas | Proxy logs / NetFlow | Herramientas de exfiltración comunes |
| Nuevos servicios, tareas programadas, software instalado | Event ID 7045, 4698 | Persistencia de malware |
| Uso de **Chisel** (tuneliza SSH sobre HTTPS port 443) | IDS / SIEM | Evasión de inspección de tráfico |
| Uso de **Cloudflared** para túneles hacia Cloudflare | DNS logs / NetFlow | Canal C2 cifrado y difícil de detectar |

#### En entornos cloud:

- Activar herramientas para detectar modificaciones a IAM, seguridad de red y recursos de datos
- Automatizar detección de anomalías: nueva regla de firewall con tráfico abierto `0.0.0.0/0` → acción automática para deshabilitar y notificar

### Pasos del lab

1. Ingresar a Blue Team Labs Online → Reto **"Ransomware"** o **"Log Analysis"**
2. Analizar los logs provistos buscando los indicadores de la tabla anterior
3. Documentar en la plantilla:

```
SISTEMA AFECTADO: _______________________
HORA PRIMER EVENTO: _____________________
INDICADOR ENCONTRADO: ___________________
TÉCNICA MITRE ATT&CK: ___________________
NIVEL DE CONFIANZA (1-10): ______________
ACCIÓN RECOMENDADA: _____________________
```

4. Si encuentran archivo cifrado o nota de rescate → subir a **ID Ransomware** para identificar variante y buscar descifrador gratuito

**Resultado esperado:** Al menos 5 indicadores identificados y documentados con técnica MITRE correspondiente.

---

## Actividad Final — Simulacro: Checklist de Respuesta CISA Completo

**Duración:** 1 hora

### Escenario

**Lunes 7:15 AM.** La coordinadora de IT recibe una llamada: "Mis archivos tienen extensión `.lockbit` y hay un mensaje en la pantalla." Al mismo tiempo el sistema de monitoreo registra tráfico SMB masivo desde la estación `PROD-PC-047` hacia el servidor `\\PROD-SRV01`. Los logs de VPN muestran un login exitoso el viernes a las 11:40 PM desde una IP de Rusia con la cuenta de un técnico de mantenimiento que fue dado de baja hace 3 semanas.

---

### Parte 2 del Checklist CISA — Paso a paso

#### Fase 1: Detección y análisis

**Paso crítico:** Determinar qué sistemas están afectados y **aislarlos inmediatamente**.

- Si múltiples sistemas o subnets están afectados → desconectar a nivel del switch
- Si no es posible desconectar la red → desconectar cable ethernet de equipos afectados o remover de Wi-Fi
- Para recursos cloud → tomar **snapshot de volúmenes** para copia forense puntual
- **Usar comunicación fuera de banda** (llamadas telefónicas, no correo interno) para coordinar — si los atacantes monitorean comunicaciones podrían moverse lateralmente o desplegar ransomware más ampliamente antes de ser contenidos
- Solo apagar dispositivos si **es imposible** aislarlos de la red — esto destruye evidencia volátil en RAM

**Triaje de sistemas:**
- Identificar y priorizar sistemas críticos para restauración en red limpia
- Confirmar naturaleza de datos en sistemas impactados
- Llevar registro de sistemas **no impactados** para despriorizarlos en restauración

**Threat hunting activo (según CISA):**
- Buscar cuentas AD nuevas o con privilegios elevados y actividad reciente
- Revisar logs de VPN para logins anómalos
- Buscar uso de `bcdedit.exe`, `vssadmin.exe`, `wbadmin.exe`, `wmic shadowcopy` — indican que el ransomware está inhabilitando recuperación
- Buscar presencia de **Cobalt Strike** (procesos legítimos de Windows con comportamiento anómalo)
- Buscar software RMM no autorizado como ejecutable portable
- Buscar volcado de LSASS / uso de Mimikatz
- Detectar posible exfiltración: volumen anormal de datos salientes, uso de Rclone/Rsync/Chisel/Cloudflared

---

#### Fase 2: Reporte y notificación

- Seguir procedimientos de notificación del IRP para involucrar equipos internos y externos
- Mantener actualizada a la **dirección** con reportes regulares conforme evoluciona la situación `[CPG 4.A]`
- Reportar el incidente a:

| Organismo | Canal | Qué reportar |
|-----------|-------|-------------|
| **CISA** | cisa.gov/report · central@cisa.dhs.gov · 1-844-729-2472 | Incidente completo, IoCs, variante |
| **FBI / IC3** | ic3.gov | Denuncia de crimen cibernético |
| **FBI Field Office** | fbi.gov/contact-us/field-offices | Asistencia local en investigación |
| **MS-ISAC** (SLTT) | soc@msisac.org · (866) 787-4722 | Para gobiernos estatales/locales |
| **CERT-MX** | gob.mx/cert | Incidentes con impacto en México |
| **INAI** | inai.org.mx | Si hay datos personales comprometidos (LFPDPPP: 72h) |

---

#### Fase 3: Contención y erradicación

**Si no hay acciones de mitigación posibles de inmediato:**
- Tomar **imagen del sistema y captura de memoria** de equipos afectados (workstations, servidores, VMs, cloud)
- Recopilar logs relevantes y muestras de malware precursor con IoCs (IPs C2, entradas de registro, archivos detectados)
- Preservar evidencia **volátil** antes de que se pierda: memoria del sistema, Windows Security logs, buffers de firewall
- Consultar a las agencias federales sobre **descifradores disponibles** — investigadores pueden haber encontrado fallas de cifrado en la variante específica

**Pasos de contención:**
1. Investigar guía de confianza para la variante específica (fuentes: US Government, MS-ISAC, vendor reputado)
2. Terminar o deshabilitar ejecución de binarios de ransomware conocidos; eliminar valores del registro y archivos asociados
3. Identificar sistemas y cuentas involucrados en la brecha inicial (incluyendo cuentas de correo)
4. Contener sistemas asociados que pueden usarse para acceso no autorizado continuo:
   - Deshabilitar VPNs, servidores de acceso remoto, SSO, activos públicos en nube
5. Si datos del servidor están siendo cifrados por workstation infectada:
   - Revisar `Computer Management > Sessions and Open Files` para identificar usuario/sistema accediendo archivos
   - Revisar propiedades de archivos cifrados o notas de rescate para identificar usuarios con ownership
   - Revisar `TerminalServices-RemoteConnectionManager` log para conexiones RDP exitosas
   - Revisar Windows Security log, SMB event logs para eventos significativos de autenticación
   - Ejecutar **Wireshark** en servidor con filtro `smb2.filename contains cryptxxx` para identificar IPs cifrando activamente

**Análisis de persistencia:**
- **Outside-in:** acceso autenticado a sistemas externos vía cuentas falsas, backdoors en perímetro, explotación de vulnerabilidades externas
- **Inside-out:** implantes de malware en red interna, uso de Cobalt Strike, PsTools (PsExec), scripts de PowerShell

**Reconstrucción:**
- Reimaginar sistemas desde **imágenes limpias preconfiguradas** (no restaurar SO desde backup)
- Usar plantillas IaC para reconstruir recursos cloud
- Emitir **reset de contraseñas** para todos los sistemas afectados
- Aplicar parches, actualizar software, implementar controles de seguridad no aplicados anteriormente
- Actualizar claves de cifrado gestionadas por el cliente si aplica

---

#### Fase 4: Recuperación y actividad post-incidente

- Reconectar sistemas y restaurar datos desde **backups offline cifrados** según priorización de servicios críticos
- Verificar que sistemas limpios no se re-infecten durante recuperación (usar VLAN de recuperación dedicada)
- Documentar **lecciones aprendidas** para actualizar políticas, planes y procedimientos
- Compartir lecciones aprendidas e IoCs relevantes con **CISA** o el ISAC del sector para beneficiar a otros

---

### Rúbrica del simulacro

| Criterio | Excelente (3) | Aceptable (2) | Necesita mejora (1) |
|---------|--------------|--------------|---------------------|
| Aislamiento inicial | < 15 min, sin apagar toda la planta | Aislado con demora o errores parciales | No aislaron o apagaron todo sin discriminar |
| Preservación forense | Capturaron RAM + logs + IoCs antes de apagar | Solo logs | No preservaron evidencia |
| Threat hunting | Identificaron ≥ 5 indicadores con MITRE mapping | 2–4 indicadores | < 2 indicadores |
| Notificación correcta | CISA + FBI + INAI con información correcta y oportuna | Notificaron 1–2 organismos | No notificaron |
| Decisión sobre rescate | No pagaron; exploraron descifradores; consultaron CISA/FBI | Indecisión fundamentada | Pagaron sin explorar alternativas |
| Cumplimiento LFPDPPP | Plan de notificación INAI en 72h con alcance documentado | Mencionaron LFPDPPP sin plan | No consideraron LFPDPPP |
| Contención de cuenta comprometida | Deshabilitaron cuenta, revocaron VPN, reset credenciales | Deshabilitaron cuenta solo | No actuaron sobre la cuenta |

**Puntaje mínimo: 15/21**

---

## Recursos CISA — Sin costo

| Recurso | Descripción | URL |
|---------|-------------|-----|
| **#StopRansomware Guide** | Guía completa (PDF) | cisa.gov/stopransomware/ransomware-guide |
| **Vulnerability Scanning** | Escaneo de vulnerabilidades sin costo | cisa.gov/cyber-resource-hub |
| **CSET / RRA** | Herramienta de evaluación de preparación ante ransomware | cisa.gov/resources-tools/services/cisa-tabletop-exercise-packages |
| **CISA KEV Catalog** | Vulnerabilidades explotadas activamente | cisa.gov/known-exploited-vulnerabilities-catalog |
| **StopRansomware.gov** | Portal central de recursos | stopransomware.gov |
| **MS-ISAC Security Primer** | Vectores comunes y recomendaciones | cisecurity.org |
| **IST Blueprint for Ransomware Defense** | Plan de acción para PYMES | ist.org |
| **No More Ransom** | Descifradores gratuitos disponibles | nomoreransom.org |
| **ID Ransomware** | Identificar variante de ransomware | id-ransomware.malwarehunterteam.com |
| **NIST Zero Trust Architecture** | SP 800-207 | csrc.nist.gov |
| **NSA Mitigating Cloud Vulnerabilities** | Guía de seguridad en nube | nsa.gov |
| **FBI IC3** | Reporte de crimen cibernético | ic3.gov |
| **CERT-MX** | Reporte en México | gob.mx/cert |
| **INAI** | Notificación de brecha de datos personales | inai.org.mx |

---

## Tarjeta de bolsillo — #StopRansomware CISA

| PREVENIR | DETECTAR | RESPONDER |
|---------|---------|----------|
| ✅ Backups offline + golden images | 🔍 vssadmin / bcdedit / wbadmin en logs | 🔴 Aislar a nivel switch — no apagar |
| ✅ MFA resistente a phishing en todo | 🔍 Cobalt Strike con nombre de proceso legítimo | 🔴 Snapshot cloud antes de aislar |
| ✅ Deshabilitar SMBv1, RDP sin MFA | 🔍 RMM como portable executable | 🔴 Comunicar fuera de banda (teléfono) |
| ✅ DMARC + DKIM + SPF activos | 🔍 LSASS dump / Mimikatz / NTDSutil | 🔴 Identificar variante → ID Ransomware |
| ✅ WDAC / AppLocker + EDR | 🔍 Rclone / Chisel / Cloudflared saliente | 🔴 Reportar CISA + FBI + INAI |
| ✅ Parcheo < 72h para CVEs activos | 🔍 Nuevos servicios / tareas programadas | 🔴 No pagar — CISA/FBI no lo recomiendan |
| ✅ Segmentación OT/IT + ZTA | 🔍 Cuentas AD nuevas con privilegios | 🔴 Reimaginar desde golden image limpia |
| ✅ Auditar y revocar MSPs/terceros | 🔍 Logins VPN nocturnos de países inusuales | 🔴 Lecciones aprendidas + actualizar IRP |

---

## Métricas de éxito del día bonus

| Métrica | Objetivo |
|---------|---------|
| RRA CISA completada con reporte exportado | 100% de equipos |
| Indicadores de threat hunting identificados en lab | ≥ 5 por equipo |
| Puntaje promedio del simulacro de respuesta | ≥ 15/21 |
| Tiempo de aislamiento en simulacro | < 15 minutos |
| Organismos de notificación correctamente identificados | CISA + FBI + INAI (3/3) |

---

*Contenido basado en: #StopRansomware Guide (CISA, FBI, NSA, MS-ISAC — septiembre 2023). Dominio público del gobierno de EE.UU.*
*Adaptado para manufactura en Ciudad Juárez — Skilling Center Tecmilenio / INDEX CJ — Marzo 2026*
