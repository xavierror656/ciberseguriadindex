# Día 4 — Respuesta a Incidentes y Ransomware

**Duración:** 4 horas
**Fecha:** Jueves 27 de marzo de 2026

---

## Objetivo del día

Desarrollar la capacidad de detectar, contener y recuperar sistemas ante ataques reales, aplicando procedimientos estructurados de respuesta a incidentes en el contexto de la industria manufacturera de Ciudad Juárez.

---

## Bloque 1 — Respuesta a incidentes en manufactura

**Duración:** 1 hora

### El costo real de un incidente en una maquiladora de Juárez

Cuando una planta manufacturera sufre un ataque, las pérdidas van mucho más allá de los costos de IT:

| Tipo de pérdida | Ejemplo en maquiladora | Costo estimado |
|----------------|----------------------|----------------|
| Producción detenida | Línea de ensamble parada 24h | $50,000–$500,000 USD |
| Penalizaciones de cliente | Ford cobra por entrega tardía de componentes | Hasta 3x el valor del pedido |
| Recuperación de sistemas | IT externo, nuevos equipos, licencias | $20,000–$200,000 USD |
| Investigación forense | Empresa especializada en IR | $15,000–$80,000 USD |
| Reputación con cliente | Riesgo de perder contrato | Millones en ingresos anuales |
| Datos de empleados comprometidos | Posible demanda colectiva | Variable |

**Caso documentado:** Planta de manufactura electrónica en Juárez (2023) — Ransomware paró producción 72 horas. Pérdida total estimada: $1.2 millones USD. El vector de entrada fue un correo de phishing abierto en una laptop de ingeniería.

---

### Las 6 fases de respuesta a incidentes (NIST SP 800-61)

#### Fase 1 — Preparación

Antes de que ocurra el ataque:

- [ ] Plan de Respuesta a Incidentes (IRP) documentado y aprobado
- [ ] Equipo de respuesta definido con roles y contactos 24/7
- [ ] Herramientas de respuesta disponibles (EDR, SIEM, backups verificados)
- [ ] Acuerdos con proveedor externo de IR (Incident Response)
- [ ] Ejercicios de simulación realizados al menos una vez al año

**Equipo mínimo de respuesta para maquiladora:**

| Rol | Responsabilidad | Quién en planta |
|-----|----------------|-----------------|
| Coordinador de IR | Dirige la respuesta, toma decisiones | Gerente de IT o CISO |
| Técnico de sistemas | Aísla sistemas, preserva evidencia | Administrador de red/sistemas |
| Enlace con negocio | Coordina impacto con producción | Gerente de planta o COO |
| Enlace legal/RRHH | Maneja comunicación y compliance | Director RRHH o abogado |
| Contacto con cliente | Notifica a clientes si aplica | Director de calidad o ventas |

#### Fase 2 — Detección e identificación

**Fuentes de detección en planta manufacturera:**

| Fuente | Qué puede detectar | Herramienta |
|--------|-------------------|-------------|
| Antivirus/EDR | Malware, comportamiento sospechoso | Defender, CrowdStrike |
| Firewall | Conexiones a IPs maliciosas, escaneos | Fortinet, Cisco, pfSense |
| Active Directory | Logins fallidos, cuentas bloqueadas | Event Viewer, Azure AD |
| Email Gateway | Phishing, malware adjunto | Defender for O365 |
| Usuario reporta | Comportamiento extraño en equipo | Helpdesk |
| Sistema lento/cifrado | Síntoma de ransomware activo | Monitoreo de performance |

**Indicadores de Compromiso (IoC) más comunes en manufactura:**

```
Red:
• Tráfico masivo a IPs externas en horarios nocturnos
• DNS queries inusuales a dominios recién registrados
• Conexiones a países sin operaciones (Rusia, Corea del Norte)
• Escaneo interno de puertos entre segmentos

Endpoint:
• Proceso desconocido consumiendo alta CPU/disco
• Archivos con extensión cambiada (.locked, .encrypted, .RYUK)
• Nuevas cuentas de administrador creadas sin ticket
• Deshabilitación de antivirus o backup

Usuario:
• Reporte de "mi equipo está lento y hay archivos que no puedo abrir"
• Correo del CEO pidiendo algo inusual
• Acceso desde ubicación geográfica imposible
```

#### Fase 3 — Contención

**Contención a corto plazo — Primeros 30 minutos:**

```
PRIORIDAD 1: Aislar sistemas afectados
  → Desconectar equipo infectado de la red (cable ethernet + WiFi)
  → NO apagar el equipo (se pierde evidencia en memoria RAM)
  → Bloquear cuenta comprometida en Active Directory

PRIORIDAD 2: Identificar alcance
  → ¿Cuántos equipos están afectados?
  → ¿Llegó a la red OT / producción?
  → ¿Se exfiltraron datos?

PRIORIDAD 3: Proteger sistemas críticos
  → Desconectar servidores de backup de la red (si el backup no está infectado)
  → Aislar servidores de ERP si hay riesgo
  → Activar modo manual en producción si sistemas MES están comprometidos
```

**Decisión crítica en planta manufacturera:** ¿Se para producción o se continúa en modo manual?

| Escenario | Decisión recomendada |
|-----------|---------------------|
| Solo afecta PCs de oficina | Continuar producción, aislar red de oficinas |
| Afecta MES pero no PLC | Producción en modo manual documentado |
| Afecta PLC / SCADA | Detener producción para evitar accidentes |
| Afecta sistema de calidad | Detener hasta restaurar o proceder con inspección 100% manual |

#### Fase 4 — Erradicación

Eliminar completamente el malware y cerrar el vector de entrada:

- Identificar y eliminar todos los archivos maliciosos
- Cerrar la vulnerabilidad que permitió el acceso inicial (parchear, cambiar credenciales)
- Restablecer todas las contraseñas de cuentas posiblemente comprometidas
- Verificar que no haya puertas traseras (backdoors) persistentes
- Revisar tareas programadas, servicios del sistema, llaves de registro

#### Fase 5 — Recuperación

**Orden de restauración en maquiladora:**

```
1. Sistemas de producción críticos (MES, SCADA) — Impacto directo en operación
2. ERP (SAP/Oracle) — Necesario para órdenes de trabajo y logística
3. Correo corporativo — Comunicación interna y con clientes
4. Servidores de archivos — Documentación técnica
5. Estaciones de trabajo — Usuarios individuales
```

**Verificación antes de reintegrar a producción:**
- Sistema restaurado desde backup limpio y verificado
- Antivirus actualizado y escaneado completo
- Parche aplicado que cerró la vulnerabilidad
- Credenciales restablecidas
- Monitoreo intensivo durante 72 horas post-recuperación

#### Fase 6 — Lecciones aprendidas

Post-mortem documentado dentro de las **2 semanas** posteriores al incidente:
- ¿Cómo entró el atacante?
- ¿Qué sistemas afectó y por qué?
- ¿Qué detección falló y por qué?
- ¿Qué controles hubieran prevenido el ataque?
- ¿Qué cambios se implementarán?

---

### Estándares aplicados

#### NIST Cybersecurity Framework

| Función | Actividad | Métrica |
|---------|-----------|---------|
| **Detect** | Identificar el ataque lo antes posible | MTTD < 24 horas |
| **Respond** | Contener y erradicar la amenaza | MTTR < 4 horas |
| **Recover** | Restaurar operaciones normales | RTO < 8 horas |

#### CIS Critical Security Controls

| Control | Descripción | Aplicación |
|---------|-------------|-----------|
| Control 17 — Incident Response | Plan y equipo de respuesta | IRP documentado y probado |
| Control 8 — Log Management | Centralizar y retener logs | SIEM con logs de 90+ días |
| Control 13 — Network Monitoring | Detectar anomalías en red | NDR o SIEM con alertas |

---

### Métricas de respuesta a incidentes

#### Mean Time to Detect (MTTD)

```
MTTD = Hora de detección − Hora de inicio del ataque
```

**Meta:** < 24 horas
**Realidad en maquiladoras sin SIEM:** 3–6 meses (promedio industria manufacturera 2024)

**Cómo mejorar MTTD:**
- Implementar EDR en todos los endpoints
- Centralizar logs en SIEM (Microsoft Sentinel disponible en M365)
- Alertas automáticas por comportamiento anómalo
- Capacitar usuarios para reportar comportamiento sospechoso

#### Mean Time to Respond (MTTR)

```
MTTR = Hora de contención − Hora de detección
```

**Meta:** < 4 horas
**Factores que aumentan el MTTR:**
- No tener plan de respuesta documentado
- No saber quién es responsable de qué
- No tener herramientas de respuesta disponibles

#### Recovery Time Objective (RTO)

```
RTO = Tiempo máximo aceptable para restaurar un sistema crítico
```

**Metas por sistema en maquiladora:**

| Sistema | RTO recomendado | Justificación |
|---------|----------------|---------------|
| Producción / MES | < 4 horas | Impacto directo en cumplimiento con cliente |
| ERP (SAP/Oracle) | < 8 horas | Necesario para operaciones del negocio |
| Correo corporativo | < 4 horas | Comunicación crítica en incidente |
| Servidores de archivos | < 24 horas | Documentación técnica |
| Estaciones de trabajo | < 48 horas | Usuarios pueden trabajar temporalmente |

#### Recovery Point Objective (RPO)

```
RPO = Máxima pérdida de datos aceptable medida en tiempo
```

**Meta para datos críticos:** < 4 horas (backups cada 4 horas como mínimo)

---

## Laboratorio 7 — Simulación de ransomware

**Duración:** 1 hora

### Objetivo
Practicar el proceso de detección, contención y respuesta ante un ataque de ransomware en entorno controlado.

### Escenario

**Empresa ficticia:** Componentes Automotrices Juárez S.A. de C.V.
**Hora:** 6:47 AM, turno nocturno terminando
**Situación:** El supervisor de IT recibe llamadas de empleados reportando que no pueden abrir archivos. En las pantallas aparece:

```
╔══════════════════════════════════════════════════════╗
║           TUS ARCHIVOS HAN SIDO CIFRADOS             ║
║                                                      ║
║  Todos tus documentos, imágenes y bases de datos     ║
║  han sido cifrados con algoritmo AES-256.            ║
║                                                      ║
║  Para recuperar tus archivos debes pagar             ║
║  85,000 USD en Bitcoin a la siguiente dirección:     ║
║  1BvBMSEYstWetqTFn5Au4m4GFg7xJaNVN2                 ║
║                                                      ║
║  Tienes 72 horas. Después el precio se duplica.      ║
║  Contacto: recovery@onionmail.org                    ║
╚══════════════════════════════════════════════════════╝
```

**Archivos afectados observados:**
```
Finanzas/presupuesto_2026.xlsx.LOCKED
Ingenieria/planos_arneses_F150.dwg.LOCKED
RRHH/nomina_marzo_2026.xlsx.LOCKED
MES/ordenes_produccion_semana12.db.LOCKED
```

### Actividad — Respuesta estructurada (60 minutos)

**Fase 1: Primeros 10 minutos — Contención inmediata**

El equipo responde como si fuera una situación real. Deben decidir y documentar:

1. ¿Qué sistemas se aíslan primero?
2. ¿Se detiene la línea de producción?
3. ¿A quién se notifica y en qué orden?
4. ¿Se apaga el servidor afectado? ¿Por qué sí o no?
5. ¿Se notifica al cliente (empresa automotriz)?

**Fase 2: Minutos 10–30 — Evaluación de alcance**

Preguntas a responder con la información disponible:
- ¿Cuántos equipos están afectados?
- ¿Llegó al servidor del MES?
- ¿Los backups están accesibles o también fueron cifrados?
- ¿Cuándo fue el último backup limpio disponible?

**Árbol de decisión — ¿Se paga el rescate?**

```
¿Tienes backups limpios disponibles?
├── SÍ → No pagar. Restaurar desde backup. Duración estimada: RTO
└── NO →
    ├── ¿El negocio puede sobrevivir sin los datos?
    │   ├── SÍ → No pagar. Reconstruir operaciones.
    │   └── NO →
    │       ├── ¿La empresa puede pagar sin comprometer continuidad?
    │       │   ├── NO → Negociar, buscar decryptors públicos (nomoreransom.org)
    │       │   └── SÍ → Decisión de alta gerencia + asesoría legal
    │       │             (pagar no garantiza recuperación)
    └── Siempre: Reportar a CERT-MX y autoridades
```

**Fase 3: Minutos 30–50 — Plan de recuperación**

Los equipos diseñan el plan de recuperación:

| Paso | Acción | Responsable | Tiempo estimado |
|------|--------|-------------|----------------|
| 1 | Verificar integridad de backups | Admin de sistemas | 30 min |
| 2 | Formatear y reinstalar SO en equipos afectados | IT | 4h por equipo |
| 3 | Restaurar MES desde backup | Admin de sistemas | 2h |
| 4 | Restaurar ERP desde backup | Admin SAP | 3h |
| 5 | Parchear vulnerabilidad de entrada | IT | 1h |
| 6 | Cambiar todas las contraseñas | IT + usuarios | 2h |
| 7 | Verificar funcionamiento y reanudar producción | IT + Producción | 1h |

**Fase 4: Minutos 50–60 — Comunicación**

¿Cómo se comunica el incidente?

- **Internamente:** ¿Qué se dice a los empleados? ¿Cuándo?
- **Al cliente (Ford, Delphi):** ¿Cuándo se notifica? ¿Qué información se comparte?
- **Regulatorio:** ¿Se debe reportar a alguna autoridad? (INAI si hay datos personales)
- **Medios:** ¿Si hay filtración de información a prensa?

---

## Laboratorio 8 — Análisis de logs con Blue Team Labs

**Duración:** 1 hora
**Plataforma:** Blue Team Labs Online

### Objetivo
Desarrollar habilidades de análisis forense de logs para identificar la cadena completa de un ataque.

### Acceso
Registro gratuito en: [https://blueteamlabs.online](https://blueteamlabs.online)

**Desafíos recomendados:**
- "The Report" — Análisis de logs de Windows
- "Phishing Analysis" — Investigación de correo malicioso
- "Browser Forensics" — Análisis de actividad de navegador

### Ejercicio adaptado — Investigación de incidente en planta de Juárez

**Situación:** Después del ransomware del Laboratorio 7, el equipo de IR necesita determinar cómo entró el atacante. Se tienen los siguientes logs disponibles:

**Log 1 — Proxy web (navegación de usuarios):**
```
2026-03-10 09:23:41 - User: jmorales - URL: http://invoice-dhl-mx.tk/track?id=7823
2026-03-10 09:23:45 - User: jmorales - URL: http://invoice-dhl-mx.tk/download/factura.exe
2026-03-10 09:24:02 - User: jmorales - File download: factura.exe (2.3 MB)
2026-03-10 09:24:15 - Antivirus: ALERT - factura.exe - Detection: Trojan.Downloader
2026-03-10 09:24:18 - Antivirus: Action: Quarantined
2026-03-10 09:25:33 - User: jmorales - URL: http://malicious-c2.ru/beacon
2026-03-10 09:25:34 - Firewall: ALLOWED - Outbound - 192.168.1.87:49234 → 185.220.101.45:443
```

**Log 2 — Active Directory:**
```
2026-03-10 09:26:01 - Account: jmorales - Lateral movement to: \\fileserver01
2026-03-10 09:26:45 - Account: jmorales - Accessed: \\fileserver01\Finanzas
2026-03-10 09:28:12 - Account: SYSTEM (fileserver01) - New scheduled task created
2026-03-10 09:28:15 - Account: SYSTEM (fileserver01) - New admin account: svc_backup2
2026-03-10 11:45:00 - Account: svc_backup2 - Login from: 185.220.101.45 (External IP!)
2026-03-10 11:45:12 - Account: svc_backup2 - Disabled backup service
2026-03-10 11:46:00 - Account: svc_backup2 - Start mass encryption process
```

**Preguntas de análisis:**

1. ¿Cuál fue el vector de entrada inicial?
2. ¿A qué hora exacta fue comprometido el sistema?
3. ¿Qué técnica usó el atacante para moverse lateralmente? (MITRE ATT&CK)
4. ¿Por qué el antivirus no detuvo el ataque si detectó el archivo?
5. ¿Qué hizo el atacante antes de activar el ransomware? ¿Por qué esperó?
6. ¿Qué logs o alertas faltaron que hubieran detectado esto antes?

**Línea de tiempo del ataque (completar):**

```
09:23 → Jmorales hace clic en enlace malicioso
09:24 → _______________________________________
09:25 → _______________________________________
09:26 → _______________________________________
09:28 → _______________________________________
11:45 → _______________________________________
11:46 → INICIO DEL CIFRADO MASIVO
```

**Correlación con MITRE ATT&CK:**

| Hora | Actividad | Táctica MITRE | Técnica |
|------|-----------|---------------|---------|
| 09:23 | Clic en phishing | Initial Access | T1566.001 |
| 09:24 | Descarga malware | __________ | ________ |
| 09:25 | Conexión a C2 | __________ | ________ |
| 09:26 | Acceso a fileserver | __________ | ________ |
| 09:28 | Nueva cuenta admin | __________ | ________ |
| 11:45 | Login externo | __________ | ________ |
| 11:46 | Ransomware activo | Impact | T1486 |

---

## Bloque 2 — Higiene Digital Básica

**Duración:** 30 minutos (integrado al inicio del Proyecto Final)

Esta sección cierra el ciclo del curso con las prácticas fundamentales que cualquier empleado de planta debe dominar, independientemente de su rol.

---

### Gestión de contraseñas

#### El problema real en maquiladoras

- El 65% de los empleados reutiliza la misma contraseña en sistemas corporativos y cuentas personales
- Cuando una base de datos externa es comprometida (LinkedIn, Adobe, etc.), los atacantes prueban esas mismas credenciales contra el ERP o VPN de la empresa
- Contraseñas comunes encontradas en ataques reales: `Empresa2024!`, `Juarez123`, `Planta@2025`

#### Gestores de contraseñas — La solución práctica

Un gestor de contraseñas almacena y genera contraseñas únicas y complejas para cada sistema. El empleado solo necesita recordar **una contraseña maestra**.

**Opciones gratuitas recomendadas:**

| Gestor | Tipo | Plataformas | Uso recomendado |
|--------|------|-------------|-----------------|
| **Bitwarden** | Open source, nube | Windows, Mac, iOS, Android | Personal y corporativo |
| **KeePass** | Local, sin nube | Windows, Linux | Entornos con restricciones de nube |
| **Microsoft Authenticator** | Corporativo | iOS, Android | Integrado con M365 |

**Características de una buena contraseña:**
```
❌ Débil:   Juarez2024
❌ Débil:   P@ssw0rd1
✅ Fuerte:  Tz9#mKpL2$vQnR8x   (generada por gestor)
✅ Fuerte:  café-luna-perro-tren (passphrase de 4 palabras)
```

**Regla de oro:** Una contraseña diferente por cada sistema. Si un atacante obtiene una, no obtiene todas.

---

### Actualizaciones de software — Por qué importan

#### Las vulnerabilidades tienen nombre y número (CVE)

Cada vulnerabilidad de seguridad descubierta recibe un identificador público: **CVE-YYYY-NNNNN**. Los atacantes buscan activamente sistemas sin parchear.

**Ejemplo real:**
- **CVE-2021-34527 (PrintNightmare)** — Vulnerabilidad crítica en Windows que permitía control total del sistema. Microsoft liberó el parche el 6 de julio de 2021. Plantas que no parchearon a tiempo fueron comprometidas semanas después.
- **CVE-2023-23397** — Vulnerabilidad en Microsoft Outlook que permitía robar credenciales sin que el usuario abriera ningún archivo. Solo recibir el correo era suficiente.

#### Tipos de actualizaciones y su urgencia

| Tipo | Ejemplo | Tiempo máximo para aplicar |
|------|---------|---------------------------|
| Crítica (CVSS ≥ 9.0) | Ejecución remota de código sin autenticación | 72 horas |
| Alta (CVSS 7.0–8.9) | Escalación de privilegios | 7 días |
| Media (CVSS 4.0–6.9) | Denegación de servicio | 30 días |
| Baja (CVSS < 4.0) | Divulgación de información limitada | 90 días |

**En maquiladoras de Juárez:** El mayor riesgo son los equipos con Windows 10 o sistemas operativos sin soporte activo. Microsoft dejó de liberar parches de seguridad para Windows 10 en octubre de 2025.

#### Buenas prácticas para empleados

**En equipos corporativos:**
- [ ] Nunca posponer reinicios por actualizaciones de Windows — hacerlo fuera del horario laboral
- [ ] Reportar a IT si el equipo lleva más de 2 semanas sin actualizarse
- [ ] No deshabilitar el antivirus aunque "el equipo esté lento"
- [ ] Actualizar apps corporativas (Teams, SAP GUI, navegadores) cuando IT lo indique

**En dispositivos personales usados para trabajo:**
- [ ] Activar actualizaciones automáticas en iOS o Android
- [ ] Actualizar apps bancarias y de trabajo regularmente
- [ ] No usar dispositivos con sistema operativo sin soporte (Android < 10, iOS < 16)

---

### Canales de reporte de incidentes

Un incidente detectado y reportado a tiempo puede evitar pérdidas millonarias. La mayoría de los ataques se propagan durante horas o días antes de ser detectados porque los empleados no saben a quién reportar.

**¿Qué debe reportar inmediatamente cualquier empleado?**

| Situación | A quién reportar | Tiempo máximo |
|-----------|-----------------|---------------|
| Correo sospechoso de phishing | IT / Helpdesk | Inmediato — no abrir adjuntos |
| Equipo lento o con archivos que no abren | IT / Helpdesk | Inmediato — no apagarlo |
| Mensaje de "tus archivos fueron cifrados" | IT + Gerente directo | Inmediato |
| Solicitud inusual de un "directivo" por WhatsApp | Verificar por teléfono antes de actuar | Antes de cualquier acción |
| Pérdida de dispositivo con acceso a correo corporativo | IT + RRHH | Dentro de 1 hora |
| Acceso accidental a información de otro departamento | IT + Supervisor | Ese mismo día |

**Principio clave:** Reportar una sospecha falsa no tiene consecuencias. No reportar un incidente real puede costar millones.

---

## Proyecto Final del Curso — Simulación completa

**Duración:** 2 horas

### Escenario integrador

**Empresa:** Aztec Electronics Manufacturing S.A. de C.V.
**Giro:** Manufactura de tableros electrónicos para la industria automotriz (cliente principal: GM y Stellantis)
**Ubicación:** Parque Industrial Bermúdez, Ciudad Juárez
**Empleados:** 1,200 personas, 3 turnos
**Sistemas:** SAP S/4HANA, MES Ignition, Active Directory, Office 365, red OT con PLCs Allen-Bradley

---

### Cronología del ataque (los equipos reciben información en etapas)

**ETAPA 1 — Lunes 8:15 AM**
El Jefe de Compras recibe este correo:

> *De: proveedores@gm-supply-mx.com*
> *"Adjunto nueva lista de precios y contrato para Q2-2026. Favor revisar y firmar digitalmente."*
> *Adjunto: Contrato_GM_Q2_2026.pdf.exe*

**Preguntas Etapa 1:**
- ¿Es este correo legítimo? ¿Por qué?
- ¿El jefe de compras debería abrir el adjunto?
- ¿Qué debe hacer en su lugar?

---

**ETAPA 2 — Lunes 8:47 AM**
El jefe de compras abrió el adjunto. Su antivirus no detectó nada. A las 9:00 AM el helpdesk recibe reporte: "Mi equipo está lento".

**Preguntas Etapa 2:**
- ¿Qué está pasando en el equipo del jefe de compras?
- ¿Qué acción inmediata debe tomar el helpdesk?
- ¿A quién más se notifica en este momento?

---

**ETAPA 3 — Lunes 11:30 AM**
Se detecta que el atacante tiene acceso a SAP con las credenciales del jefe de compras. En las últimas 2 horas realizó:
- Consulta de 847 órdenes de compra activas
- Descarga de lista completa de proveedores con datos bancarios
- Intento (fallido) de modificar una transferencia de $220,000 USD

**Preguntas Etapa 3:**
- ¿Qué datos fueron comprometidos?
- ¿Qué deben hacer con las órdenes de compra activas?
- ¿Se debe notificar a los proveedores? ¿Cuándo?
- ¿Qué controles hubieran prevenido el acceso a SAP?

---

**ETAPA 4 — Lunes 3:00 PM**
El atacante escaló privilegios y ahora tiene acceso de administrador de dominio. Se detecta movimiento lateral hacia el servidor del MES. La línea de producción Turno 2 reporta que la pantalla de su HMI muestra datos incorrectos.

**Preguntas Etapa 4:**
- ¿Se detiene la producción? Justificar.
- ¿Cómo se aísla el MES sin detener toda la operación?
- ¿Qué riesgo representa que el HMI muestre datos incorrectos?
- ¿Cómo se coordina con el cliente (GM) en este momento?

---

**ETAPA 5 — Lunes 6:00 PM**
Contenido el ataque. El MES fue aislado. La producción está en modo manual con papelerío. El equipo de IR externo llega a las 9:00 PM. Se confirma que no hubo cifrado de archivos, pero sí exfiltración de datos de proveedores.

**Entregables del proyecto final:**

**1. Análisis con MITRE ATT&CK (30 minutos)**
Crear matriz de tácticas y técnicas utilizadas en cada etapa del ataque.

**2. Aplicación de controles CIS (20 minutos)**
Para cada técnica de MITRE, identificar qué control CIS lo hubiera prevenido o mitigado.

**3. Plan de respuesta al incidente (30 minutos)**
Documentar el IRP ejecutado durante la simulación:
- Línea de tiempo de acciones tomadas
- Decisiones tomadas y justificación
- Comunicaciones realizadas

**4. Reporte post-mortem (20 minutos)**
Documento ejecutivo de 1 página para presentar a la dirección de la planta:
- ¿Qué pasó?
- ¿Qué datos se vieron comprometidos?
- ¿Qué se hizo para contener?
- ¿Qué cambios se implementarán?

**5. Presentación ejecutiva (20 minutos)**
Cada equipo presenta sus hallazgos en 5 minutos. Incluir:
- 3 controles prioritarios que hubieran prevenido el ataque
- Inversión estimada para implementarlos
- ROI de la inversión vs costo del incidente

---

## Evaluación final del curso

| Criterio | Peso | Descripción |
|----------|------|-------------|
| Desempeño en laboratorios | 30% | Correctitud y metodología en labs 1–8 |
| Análisis MITRE ATT&CK | 20% | Mapeo correcto de tácticas del proyecto final |
| Diseño de controles | 20% | Calidad y aplicabilidad de controles propuestos |
| Plan de respuesta | 20% | Estructura y coherencia del IRP |
| Presentación ejecutiva | 10% | Claridad y relevancia para negocio |

---

## Recursos para continuar aprendiendo

### Plataformas gratuitas
- **TryHackMe:** [https://tryhackme.com](https://tryhackme.com) — Rutas: SOC Level 1, Cyber Defense
- **Blue Team Labs:** [https://blueteamlabs.online](https://blueteamlabs.online)
- **OWASP Juice Shop:** Instalar localmente con Docker para práctica continua
- **OverTheWire:** [https://overthewire.org](https://overthewire.org) — Bandit completo (niveles 0–34)

### Recursos específicos para OT/ICS
- **CISA ICS Training:** [https://www.cisa.gov/ics-training](https://www.cisa.gov/ics-training) — Gratuito
- **SANS ICS curriculum:** Cursos especializados en seguridad industrial

### Estándares para profundizar
- NIST CSF 2.0 — Descarga gratuita en nist.gov
- CIS Controls v8 — Descarga gratuita en cisecurity.org
- MITRE ATT&CK for ICS — [https://attack.mitre.org/matrices/ics/](https://attack.mitre.org/matrices/ics/)

### Alertas y noticias de amenazas
- **CERT-MX:** [https://www.gob.mx/cert](https://www.gob.mx/cert) — Alertas para México
- **CISA Alerts:** [https://www.cisa.gov/news-events/cybersecurity-advisories](https://www.cisa.gov/news-events/cybersecurity-advisories)
- **Krebs on Security:** krebsonsecurity.com — Cobertura de incidentes reales

---

## Resumen del día 4 y del curso

| Elemento | Detalle |
|----------|---------|
| Temas cubiertos | Ransomware, respuesta a incidentes, higiene digital, canales de reporte |
| Estándares aplicados | NIST CSF (Detect/Respond/Recover), CIS Controls 8/13/17, NIST SP 800-61 |
| Plataformas usadas | Blue Team Labs Online |
| Métricas aprendidas | MTTD, MTTR, RTO, RPO |
| Contexto local | Automotriz, maquiladoras de Juárez, gestores de contraseñas, actualizaciones críticas |

---

## Resultados del curso — Lo que ahora puedes hacer

Al completar este curso de 16 horas puedes:

- **Identificar** correos de phishing con IA, deepfakes y ataques BEC dirigidos a maquiladoras
- **Aplicar** estándares internacionales (MITRE, CIS, NIST, ISO 27001, IEC 62443) en tu planta
- **Usar métricas** para medir y comunicar el nivel de seguridad a la dirección
- **Proteger** sistemas industriales OT/IT con arquitectura Zero Trust y segmentación
- **Responder** a incidentes de ransomware con un proceso estructurado y documentado
- **Diseñar** controles preventivos adaptados al contexto de manufactura en Juárez

---

*Curso: Ciberseguridad para la Industria Manufacturera — INDEX Ciudad Juárez*
*24–27 de marzo de 2026*
