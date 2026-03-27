# Día Bonus — Especialidades y Roles en Ciberseguridad para la Manufactura

**Basado en:** "Las diferentes especialidades dentro de la ciberseguridad" — Boreal Security (2025)
**Fuente:** https://boreal-security.com/es/post/las-diferentes-especialidades-dentro-de-la-ciberseguridad
**Audiencia:** IT, ingeniería, calidad, administración y dirección — industria manufacturera
**Duración sugerida:** 4 horas

---

## Contexto

Según un reporte de Huilihan Lokey (marzo 2025), el costo promedio internacional de un ciberataque para empresas asciende a **14.5 millones de euros**. En el entorno manufacturero de Ciudad Juárez, donde la interconexión de sistemas OT/IT, el alto flujo de personal y la dependencia de proveedores externos amplifican la superficie de ataque, conocer quién protege qué — y qué especialistas se necesitan — es tan crítico como el propio control técnico.

Este módulo bonus responde una pregunta que toda maquiladora debería contestar: **¿quién en tu organización es responsable de cada capa de seguridad?**

---

## Bloque 1 — Las ramas de la ciberseguridad y sus roles

**Duración:** 1 hora

---

### Los 4 tipos de ciberseguridad

Toda estrategia de ciberseguridad empresarial opera sobre cuatro ramas fundamentales. En manufactura, cada una tiene implicaciones directas en la continuidad operativa de la planta:

| Rama | Qué protege | Ejemplo en maquiladora |
|------|------------|----------------------|
| **Seguridad de redes** | Previene intrusiones no autorizadas a la red corporativa y OT | Segregar la red de planta (Ethernet industrial) de la red de oficinas; bloquear acceso externo a PLCs |
| **Seguridad de aplicaciones** | Mantiene la seguridad del software y previene vulnerabilidades en el desarrollo | Validar el ERP (SAP/Oracle) ante SQLi; auditar aplicaciones de control de calidad con acceso a bases de datos de producción |
| **Seguridad de la información** | Protege datos ante acceso no autorizado, uso indebido, modificación o destrucción | Cifrar archivos de diseño CAD, fórmulas de producto, datos de nómina y contratos con clientes OEM |
| **Recuperación ante desastres** | Prepara planes de acción para minimizar riesgos y recuperar operaciones rápidamente | Plan BCP para continuar línea de producción si el MES (Manufacturing Execution System) queda fuera de servicio por ransomware |

> En muchas maquiladoras medianas, una sola persona (el "jefe de IT") carga con responsabilidades de las 4 ramas. Esto es un riesgo operacional: la especialización reduce el tiempo de detección y respuesta.

---

### Servicios de ciberseguridad disponibles

Cuando una planta no tiene capacidad interna suficiente, puede contratar estos servicios especializados:

| Servicio | Descripción | Cuándo lo necesita una maquiladora |
|---------|------------|----------------------------------|
| **Informática forense** | Obtiene datos de dispositivos electrónicos y sistemas de almacenamiento para generar reportes judicialmente válidos | Robo de propiedad intelectual por ex-empleado; fuga de planos CAD a competidor |
| **Computación forense** | Analiza sistemas y redes para determinar qué ocurrió en un ataque e identificar a los responsables | Post-incidente de ransomware: reconstruir la cadena de ataque para cumplir con seguros y autoridades |
| **Servicios de seguridad de red** | Desarrolla planes de ciberseguridad para proteger la red de la empresa | Implementar segmentación OT/IT o ZTA en planta con red plana legada |
| **Investigación de cibercrimen** | Atiende violaciones al código penal: fraude, estafa, sabotaje, espionaje, robo de identidad | Fraude del CEO (BEC) hacia proveedor; extorsión digital de ex-empleado |
| **Hacking ético** | Realiza pruebas de penetración para identificar vulnerabilidades explotables | Auditoría anual de perímetro antes de certificación ISO 27001 o auditoría de cliente OEM |
| **Auditorías y consultoría** | Asesora a empresas en análisis de riesgos y desarrolla estrategias a medida | Cumplimiento LFPDPPP, preparación para certificación, evaluación de riesgo en nueva línea de producción |
| **Productos de software especializados** | Soluciones tecnológicas orientadas a seguridad | EDR, SIEM, PAM, DLP adaptados al entorno industrial |

---

### Los 11 roles profesionales en ciberseguridad

El ecosistema de ciberseguridad comprende perfiles muy distintos. Conocerlos permite que una planta decida qué contratar internamente y qué tercerizar:

| # | Rol | Responsabilidades clave | ¿Interno o tercero? |
|---|-----|------------------------|---------------------|
| 1 | **Técnico en ciberseguridad** | Soporte operativo diario: parcheo, respuesta a alertas, gestión de herramientas de seguridad | Interno — necesidad diaria |
| 2 | **Administrador de seguridad de redes** | Configura firewalls, VLANs, IDS/IPS; gestiona accesos VPN y segmentación OT/IT | Interno o MSP de confianza |
| 3 | **Arquitecto de sistemas de seguridad digital** | Diseña la arquitectura de seguridad completa: ZTA, IAM, modelo de red defensiva | Tercero o consultor externo |
| 4 | **Gerente de sistemas de seguridad** | Supervisa todos los controles técnicos y al equipo de seguridad | Interno — rol directivo |
| 5 | **Gerente de seguridad perimetral** | Administra la defensa del perímetro: firewall, WAF, proxies, DMZ | Interno o MSSP |
| 6 | **Consultor de seguridad y analista de riesgos** | Evalúa riesgos, propone controles, realiza análisis de impacto al negocio | Tercero periódico |
| 7 | **Auditor de seguridad IT** | Valida cumplimiento de políticas, frameworks (ISO 27001, NIST) y regulaciones (LFPDPPP) | Tercero — independencia requerida |
| 8 | **Asesor de seguridad IT** | Orienta a la dirección sobre inversiones, prioridades y postura estratégica | Tercero o CISO virtual |
| 9 | **Especialista en software de seguridad** | Integra, configura y mantiene herramientas: SIEM, EDR, DLP, PAM | Interno o proveedor de solución |
| 10 | **Consultor de hacking ético** | Ejecuta pentests, Red Team exercises y simulaciones de ataque | Tercero certificado (OSCP, CEH) |
| 11 | **Investigador / detective informático** | Investiga incidentes graves, fraudes digitales y delitos cibernéticos con valor forense | Tercero especializado post-incidente |

---

### Mapeo de roles a los 4 días del curso

Cada sesión de este curso cubre el dominio técnico de uno o más de estos roles:

| Día | Tema | Roles directamente relevantes |
|-----|------|------------------------------|
| Día 1 — IA & Ingeniería Social | Amenazas de phishing, deepfakes, CEO fraud | Técnico en ciberseg., Asesor IT, Analista de riesgos |
| Día 2 — Identidad & Zero Trust | MFA, PAM, Zero Trust Architecture | Administrador de redes, Gerente de seguridad perimetral, Arquitecto |
| Día 3 — Datos, Nube & Híbrido | BYOD, VPN, MDM, LFPDPPP | Especialista en software, Auditor IT, Consultor de riesgos |
| Día 4 — Respuesta a Incidentes | NIST SP 800-61, ransomware, higiene digital | Técnico, Gerente de seguridad, Investigador forense |

---

### Brechas comunes en maquiladoras medianas

| Brecha | Riesgo resultante | Solución |
|--------|------------------|---------|
| IT generalista sin especialización en seguridad | MTTD > 72 horas; sin baseline de tráfico normal | Capacitación o contratar técnico de ciberseguridad dedicado |
| Sin arquitecto de seguridad | Red plana: compromiso de un equipo = compromiso total | Contratar consultor externo para diseñar segmentación |
| Sin auditor independiente | Cumplimiento ISO/LFPDPPP no verificado externamente | Auditoría anual por tercero certificado |
| Sin plan de respuesta documentado | Improvisación en incidente = mayor daño y multas | Contratar consultor para redactar IRP (ver Día 4) |
| MSP con acceso total sin restricciones | Vector de entrada para ransomware multi-cliente | Mínimo privilegio + SLAs de seguridad en contrato |

---

### MITRE ATT&CK — ¿Qué rol defiende qué táctica?

| Táctica MITRE | Técnica ejemplo | Rol responsable de mitigación |
|--------------|----------------|------------------------------|
| Initial Access (TA0001) | T1566 Phishing | Técnico en ciberseg. + capacitación |
| Credential Access (TA0006) | T1003 OS Credential Dumping | Administrador de redes + PAM |
| Lateral Movement (TA0008) | T1021 Remote Services | Gerente de seguridad perimetral |
| Exfiltration (TA0010) | T1048 Exfiltration over Alt Protocol | Especialista en software (DLP) |
| Impact (TA0040) | T1486 Data Encrypted for Impact | Técnico + backups + IRP |

---

## Lab 1 — Mapeo de roles con el NIST NICE Framework

**Plataforma:** NIST NICE Framework + CyberSeek
**Acceso gratuito:** https://www.nist.gov/system/files/documents/2020/11/30/NICE_Framework_v1.0.pdf · https://www.cyberseek.org/pathway.html
**Duración:** 1 hora

### Objetivo

Usar el **NIST NICE Cybersecurity Workforce Framework (NICE)** para mapear los roles de ciberseguridad de tu planta, identificar brechas y trazar rutas de desarrollo profesional para el personal existente.

### Contexto del NICE Framework

El NICE Framework categoriza los roles de ciberseguridad en **7 categorías** y **52 roles de trabajo** (Work Roles), cada uno con Knowledge, Skills & Abilities (KSAs) definidos. Es el estándar de EE.UU. para describir roles y es compatible con MITRE ATT&CK.

| Categoría NICE | Función principal |
|---------------|-----------------|
| **Securely Provision (SP)** | Diseña y construye sistemas seguros |
| **Operate & Maintain (OM)** | Administra y asegura infraestructura |
| **Oversee & Govern (OV)** | Liderazgo, política, legal, auditoría |
| **Protect & Defend (PR)** | Detección y respuesta a amenazas |
| **Analyze (AN)** | Threat intelligence y análisis forense |
| **Collect & Operate (CO)** | Operaciones ofensivas/defensivas |
| **Investigate (IN)** | Investigación de incidentes y forense |

### Pasos

**Parte A — Inventario de roles actuales en tu planta (25 min)**

1. Abrir la hoja de trabajo proporcionada (o usar papel)
2. Listar a todo el personal con responsabilidades de IT/seguridad en tu organización:

```
NOMBRE: _______________________
CARGO ACTUAL: _________________
RESPONSABILIDADES DE SEGURIDAD ACTUALES: ___________________
CERTIFICACIONES / FORMACIÓN EN SEGURIDAD: __________________
```

3. Para cada persona, asignar el rol NICE más cercano usando la tabla:

| Rol NICE | Equivalente en maquiladora |
|---------|--------------------------|
| Systems Administrator | Administrador de IT general |
| Cyber Defense Analyst | Técnico de ciberseguridad / SOC |
| Cyber Defense Infrastructure Support | Administrador de redes / firewalls |
| Security Architect | Arquitecto de seguridad |
| Privacy Officer | Responsable LFPDPPP / INAI |
| Incident Responder | Coordinador de respuesta a incidentes |
| Vulnerability Assessment Analyst | Auditor / pentester interno |

**Parte B — Identificación de brechas (20 min)**

4. Marcar en la tabla qué roles NICE están **cubiertos**, **parcialmente cubiertos** o **ausentes** en tu organización:

| Rol NICE crítico | Estado en tu planta | Riesgo si está ausente |
|-----------------|--------------------|-----------------------|
| Cyber Defense Analyst | ☐ Cubierto ☐ Parcial ☐ Ausente | MTTD > 72h; sin alertas activas |
| Incident Responder | ☐ Cubierto ☐ Parcial ☐ Ausente | Improvisación ante ransomware |
| Privacy Officer | ☐ Cubierto ☐ Parcial ☐ Ausente | Incumplimiento LFPDPPP; multa INAI |
| Security Architect | ☐ Cubierto ☐ Parcial ☐ Ausente | Red plana; sin ZTA |
| Vulnerability Analyst | ☐ Cubierto ☐ Parcial ☐ Ausente | CVEs sin parchear > 72h |

**Parte C — CyberSeek: rutas de carrera (15 min)**

5. Ingresar a https://www.cyberseek.org/pathway.html
6. Explorar la ruta de carrera desde el rol actual de cada miembro del equipo hacia el rol objetivo
7. Anotar: ¿qué certificación o habilidad está entre el rol actual y el objetivo?

```
PERSONA: _______________________
ROL ACTUAL (NICE): ______________
ROL OBJETIVO (NICE): ____________
BRECHA DE CERTIFICACIÓN: ________
PLATAFORMA DE CAPACITACIÓN GRATUITA: ___________
```

**Resultado esperado:** Tabla de brechas completada; al menos 1 ruta de desarrollo identificada por miembro del equipo de IT.

---

## Lab 2 — Exploración de plataformas de capacitación y habilidades prácticas

**Plataforma:** TryHackMe (rutas de carrera gratuitas)
**Acceso gratuito:** https://tryhackme.com
**Duración:** 1 hora

### Objetivo

Explorar las rutas de aprendizaje de TryHackMe alineadas a los roles identificados en el Lab 1 y completar el **módulo de orientación** de la ruta más relevante para el equipo.

### Rutas de TryHackMe recomendadas por rol

| Rol objetivo | Ruta TryHackMe | Nivel |
|-------------|---------------|-------|
| Técnico en ciberseguridad | **Pre-Security** (gratis) | Principiante |
| Analista de defensa / SOC | **SOC Level 1** (gratis) | Intermedio |
| Administrador de redes | **Jr Penetration Tester** (gratis) | Intermedio |
| Respondedor de incidentes | **Cyber Defense** (gratis) | Intermedio |
| Investigador forense | **Jr Security Analyst** (gratis) | Principiante |

### Pasos

1. Crear cuenta gratuita en https://tryhackme.com
2. Seleccionar la ruta correspondiente al rol objetivo identificado en Lab 1
3. Completar la **primera sala (room)** de la ruta:
   - Leer el material teórico
   - Responder las preguntas del módulo
   - Anotar el score obtenido

4. Documentar la experiencia:

```
RUTA SELECCIONADA: _______________________
PRIMERA SALA COMPLETADA: ________________
SCORE OBTENIDO: __________________________
CONCEPTO NUEVO MÁS RELEVANTE PARA MI PLANTA: ___________
HABILIDAD QUE NECESITO DESARROLLAR PARA ESTE ROL: _______
```

5. Explorar el **"Learning Paths"** de TryHackMe y comparar con las rutas de CyberSeek del Lab 1:
   - ¿Cubren las mismas habilidades?
   - ¿Hay certificaciones reconocidas al final de cada ruta?

### Certificaciones de bajo costo relevantes para manufactura

| Certificación | Organismo | Costo aprox. | Rol objetivo |
|--------------|-----------|-------------|-------------|
| **CompTIA Security+** | CompTIA | ~$350 USD | Técnico en ciberseg. |
| **CompTIA CySA+** | CompTIA | ~$380 USD | Analista de defensa |
| **Google Cybersecurity Certificate** | Google/Coursera | Gratis (audit) | Entrada al campo |
| **CEH (Certified Ethical Hacker)** | EC-Council | ~$1,199 USD | Hacking ético |
| **CISM** | ISACA | ~$760 USD | Gerente / CISO |
| **ISO 27001 Lead Implementer** | PECB/BSI | ~$500-800 USD | Auditor / consultor |

**Resultado esperado:** Primera sala de TryHackMe completada; brecha de certificación identificada y documentada para al menos 2 personas del equipo.

---

## Actividad Final — Diseño del equipo de ciberseguridad ideal para tu planta

**Duración:** 1 hora

### Escenario

**Contexto:** Tu empresa acaba de recibir una notificación de un cliente OEM norteamericano: a partir de enero 2027, todos los proveedores Tier 1 y Tier 2 deberán demostrar cumplimiento con **NIST CSF 2.0** y tener designado un responsable de ciberseguridad identificable. Además, el área de calidad detectó que 3 equipos de la línea de producción están conectados directamente a internet sin firewall intermedio — una vulnerabilidad crítica.

Tu equipo tiene **60 minutos** para diseñar la estructura de ciberseguridad que necesita la planta.

---

### Parte 1 — Organigrama de ciberseguridad (20 min)

Diseñar el organigrama ideal para una planta de 500-1,500 empleados con los siguientes parámetros:

- **Presupuesto disponible:** 2 FTE internos + presupuesto para 2 servicios externos
- **Prioridad 1:** Cumplimiento NIST CSF 2.0 para cliente OEM
- **Prioridad 2:** Proteger red OT (PLCs, SCADA) ante acceso no autorizado
- **Prioridad 3:** Cumplimiento LFPDPPP (datos de nómina, empleados, clientes)

Usar esta plantilla:

```
DIRECTOR DE IT (existente)
  └── [ROL 1 INTERNO]: _______________________
       Responsabilidades: ____________________
       Certificación mínima: _________________
  └── [ROL 2 INTERNO]: _______________________
       Responsabilidades: ____________________
       Certificación mínima: _________________
  └── [SERVICIO EXTERNO 1]: __________________
       Frecuencia: __________________________
       Entregable esperado: _________________
  └── [SERVICIO EXTERNO 2]: __________________
       Frecuencia: __________________________
       Entregable esperado: _________________
```

---

### Parte 2 — Matriz de responsabilidades RACI (20 min)

Completar la matriz RACI para los procesos de seguridad críticos:

| Proceso | Interno ROL 1 | Interno ROL 2 | Externo 1 | Externo 2 | Dirección |
|---------|--------------|--------------|-----------|-----------|-----------|
| Parcheo mensual de sistemas | | | | | |
| Revisión de logs / SIEM | | | | | |
| Respuesta a incidente activo | | | | | |
| Auditoría anual LFPDPPP | | | | | |
| Pentest anual de perímetro | | | | | |
| Capacitación a empleados | | | | | |
| Reporte a INAI (si aplica) | | | | | |
| Revisión de proveedores/MSPs | | | | | |

*RACI: R = Responsable, A = Accountable, C = Consultado, I = Informado*

---

### Parte 3 — Presentación y Gallery Walk (20 min)

Cada equipo presenta su organigrama y RACI en 3 minutos. Los demás equipos evalúan usando esta rúbrica:

| Criterio | Excelente (3) | Aceptable (2) | Necesita mejora (1) |
|---------|--------------|--------------|---------------------|
| Cobertura de los 4 tipos de ciberseguridad | Los 4 cubiertos con rol asignado | 3 de 4 cubiertos | 2 o menos |
| Factibilidad presupuestaria | Respeta 2 FTE + 2 externos | Excede por 1 recurso | No viable |
| Cumplimiento NIST CSF 2.0 | Todas las funciones NIST asignadas | 3 de 5 funciones | Menos de 3 |
| Cumplimiento LFPDPPP | Privacy Officer designado con plan INAI | Mencionado sin designación | Ausente |
| RACI completo y coherente | Sin celdas vacías; sin solapamientos | Vacíos menores | Vacíos mayores o contradicciones |
| Realismo para maquiladora | Ejemplos concretos del entorno manufacturero | Genérico pero viable | Sin contexto de planta |

**Puntaje mínimo: 15/18**

---

## Recursos — Sin costo

| Recurso | Descripción | URL |
|---------|-------------|-----|
| **NIST NICE Framework** | Marco de roles y habilidades en ciberseguridad | nist.gov/cyberframework |
| **CyberSeek** | Mapa interactivo de rutas de carrera y demanda laboral | cyberseek.org/pathway.html |
| **TryHackMe** | Plataforma de capacitación práctica con rutas guiadas | tryhackme.com |
| **Google Cybersecurity Certificate** | Certificado de entrada (audit gratuito en Coursera) | grow.google/certificates |
| **CompTIA CertMaster Learn** | Recursos de estudio para Security+ y CySA+ | comptia.org |
| **ISACA Learning** | Recursos para CISM, CRISC, CISA | isaca.org |
| **NIST CSF 2.0** | Marco de ciberseguridad actualizado (2024) | nist.gov/cyberframework |
| **Boreal Security — Blog** | Especialidades y tendencias en ciberseguridad (en español) | boreal-security.com/es |
| **INAI** | Obligaciones LFPDPPP para empresas | inai.org.mx |
| **CERT-MX** | Alertas y recursos de respuesta a incidentes en México | gob.mx/cert |

---

## Tarjeta de bolsillo — Especialidades de Ciberseguridad

| LOS 4 TIPOS | LOS 11 ROLES | CUÁNDO CONTRATAR EXTERNO |
|-------------|-------------|--------------------------|
| 🔵 Seguridad de redes | Técnico en ciberseg. | Hacking ético (pentest anual) |
| 🔵 Seguridad de aplicaciones | Administrador de redes | Auditoría ISO/LFPDPPP |
| 🔵 Seguridad de la información | Arquitecto de seguridad | Investigación forense post-incidente |
| 🔵 Recuperación ante desastres | Gerente de seguridad | Consultor de riesgos (periódico) |
| **BRECHAS MÁS COMUNES** | Gerente de seguridad perimetral | CISO virtual si < 200 empleados IT |
| Sin analista de defensa dedicado | Consultor / analista de riesgos | **MARCO DE REFERENCIA** |
| Sin Privacy Officer LFPDPPP | Auditor de seguridad IT | NIST NICE para roles |
| Sin IRP documentado | Asesor de seguridad IT | NIST CSF 2.0 para funciones |
| MSP sin contrato de seguridad | Especialista en software | CyberSeek para rutas de carrera |
| Red plana sin segmentación OT/IT | Consultor hacking ético | TryHackMe para capacitación gratis |
| **COSTO PROMEDIO DE ATAQUE** | Investigador forense | **REFERENCIA LEGAL MÉXICO** |
| €14.5M (Huilihan Lokey 2025) | → Designar responsable por rol | LFPDPPP · Notif. INAI 72h |

---

## Métricas de éxito del día bonus

| Métrica | Objetivo |
|---------|---------|
| Roles NICE mapeados al personal actual | 100% del equipo de IT |
| Brechas de rol identificadas | ≥ 2 roles críticos sin cobertura documentados |
| Primera sala TryHackMe completada | 100% de participantes |
| Organigrama de ciberseguridad diseñado | 1 por empresa/equipo |
| RACI completado sin celdas vacías | 100% de los procesos cubiertos |
| Puntaje promedio del ejercicio final | ≥ 15/18 |

---

*Contenido basado en: "Las diferentes especialidades dentro de la ciberseguridad" — Boreal Security (2025).*
*Complementado con NIST NICE Cybersecurity Workforce Framework (NIST SP 800-181r1) y NIST CSF 2.0.*
*Adaptado para manufactura en Ciudad Juárez — Skilling Center Tecmilenio / INDEX CJ — Marzo 2026*
