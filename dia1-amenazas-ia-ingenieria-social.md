# Día 1 — Amenazas Emergentes con IA e Ingeniería Social

**Duración:** 4 horas
**Fecha:** Lunes 24 de marzo de 2026

---

## Objetivo del día

Comprender cómo los atacantes utilizan inteligencia artificial e ingeniería social para infiltrarse en empresas manufactureras de Ciudad Juárez, y desarrollar la capacidad de identificar y responder a estas amenazas.

---

## Bloque 1 — Panorama de amenazas en la industria maquiladora

**Duración:** 1 hora

### ¿Por qué Ciudad Juárez es un objetivo?

Ciudad Juárez concentra más de **300 plantas maquiladoras** con operaciones para empresas como Foxconn, Lear Corporation, Delphi, Bosch, Honeywell y GE Aviation. Esta densidad industrial la convierte en un objetivo atractivo por:

- Transferencias internacionales frecuentes (USD, MXN) entre corporativos en EE. UU. y plantas en México
- Acceso a propiedad intelectual de manufactura (diseños, procesos, especificaciones técnicas)
- Dependencia de proveedores locales con menor madurez en ciberseguridad
- Comunicación constante por correo electrónico entre ingeniería, compras, finanzas y corporativos

---

### Evolución del phishing — De genérico a ultraespecífico

#### Phishing tradicional (2015–2020)
Correos masivos con errores ortográficos, dominios genéricos y mensajes genéricos como "Actualiza tu contraseña".

#### Spear phishing con IA (2024–presente)
Los atacantes utilizan IA para:

- Analizar LinkedIn de empleados de la planta para conocer nombres, cargos y relaciones
- Redactar correos en español mexicano sin errores, con tono corporativo correcto
- Imitar el estilo de escritura del gerente de finanzas o del director de planta
- Automatizar ataques a cientos de empleados simultáneamente con mensajes personalizados

**Ejemplo real adaptado a Ciudad Juárez:**

> *De: carlos.mendoza@lear-corp.mx.supply-chain.net*
> *Para: Accounts.Payable@lear.com.mx*
>
> "Hola Gabriela, por instrucciones del VP de Finanzas en Detroit necesitamos confirmar una transferencia urgente de $47,000 USD al proveedor Autopartes del Norte S.A. antes del cierre de mes. El pago debe procesarse hoy. Te mando los datos bancarios por separado. Favor de no comentar con nadie más por auditoría interna."

**Señales de alerta en este correo:**
- Dominio falso: `lear-corp.mx.supply-chain.net` vs el real `lear.com`
- Urgencia artificial ("hoy", "cierre de mes")
- Solicitud de confidencialidad para evitar verificación
- Instrucción de recibir datos bancarios fuera del sistema

---

### Fraude corporativo BEC en maquiladoras

**Business Email Compromise (BEC)** es el ataque más costoso para la industria manufacturera. El FBI reporta pérdidas globales superiores a **$55 mil millones USD** entre 2013 y 2023.

**Variantes comunes en plantas de Juárez:**

| Variante | Descripción | Ejemplo local |
|----------|-------------|---------------|
| Fraude de CEO | Atacante suplanta al director de planta | Correo del "Director General" pidiendo transferencia a socio en EE. UU. |
| Fraude de proveedor | Atacante suplanta a proveedor legítimo | "Autopartes Visión" informa cambio de cuenta bancaria |
| Fraude de nómina | Atacante suplanta a RRHH o empleado | Empleado "solicita" cambio de cuenta CLABE para depósito de nómina |
| Fraude de abogado | Atacante finge ser despacho legal | Notificación urgente de demanda que requiere pago inmediato |

---

### Ataques con inteligencia artificial generativa

#### Voice cloning — Clonación de voz
Con tan solo **3 segundos de audio** de una persona (disponible en videos de LinkedIn, YouTube, conferencias), la IA puede clonar su voz con alta fidelidad.

**Caso de uso malicioso en manufactura:**
1. Atacante obtiene audio del Director de Operaciones de una presentación en LinkedIn
2. Genera mensaje de voz clonado: *"Soy [Nombre], necesito que proceses un pago urgente a este proveedor, te llamo del aeropuerto y no tengo acceso al correo"*
3. Envía el audio por WhatsApp al jefe de finanzas de la planta

**Plataformas utilizadas por atacantes:** ElevenLabs, Resemble AI, Descript (mal uso de herramientas legítimas)

#### Deepfakes en videollamadas
Herramientas como DeepFaceLab permiten a atacantes sustituir su cara en tiempo real durante una videollamada de Teams o Zoom.

**Señales de deepfake en videollamadas:**
- Bordes borrosos o difusos alrededor del cabello y orejas
- Movimiento de boca desincronizado con el audio
- Falta de parpadeo natural (menos de 15 veces por minuto)
- Sombras inconsistentes con la iluminación del fondo
- Pixelación cuando la persona gira la cabeza

---

### Ataques a cadena de suministro

Las maquiladoras en Juárez trabajan con redes de cientos de proveedores locales (transporte, mantenimiento, componentes, servicios). Muchos de estos proveedores tienen seguridad deficiente.

**Vector de ataque típico:**
1. Atacante compromete el correo de `proveedores-confiables@mantenimientoind.com.mx`
2. Desde esa cuenta legítima envía factura falsa o malware a la planta
3. El receptor confía en el remitente por ser un proveedor conocido

**Sectores más atacados en la cadena de suministro de Juárez:**
- Empresas de transporte y logística (rutas de materiales entre EE. UU. y México)
- Proveedores de mantenimiento industrial con acceso físico a planta
- Agencias aduanales con acceso a datos de importación/exportación
- Maquiladoras medianas que proveen componentes a Tier 1 automotriz

---

### Estándares aplicados

#### MITRE ATT&CK — Tácticas del día

| ID | Táctica | Técnica relevante |
|----|---------|-------------------|
| TA0001 | Initial Access | T1566 — Phishing |
| TA0001 | Initial Access | T1566.001 — Spear Phishing Link |
| TA0001 | Initial Access | T1566.002 — Spear Phishing Attachment |
| TA0006 | Credential Access | T1110 — Brute Force |
| TA0043 | Reconnaissance | T1591 — Gather Victim Org Information |

#### CIS Critical Security Controls

- **Control 14 — Security Awareness:** Capacitación continua con simulaciones de phishing reales
- **Control 9 — Email Protection:** Implementar DMARC, DKIM y SPF en dominios corporativos
- **Control 5 — Account Management:** Verificación de identidad para cambios de datos bancarios

---

### Métricas de seguridad — Bloque 1

#### Phishing Click Rate

```
Phishing Click Rate = (Usuarios que hicieron clic / Total de usuarios) × 100
```

| Nivel | Valor | Acción recomendada |
|-------|-------|--------------------|
| Alto riesgo | > 15% | Capacitación inmediata + simulaciones semanales |
| Riesgo moderado | 5% – 15% | Reforzar entrenamiento mensual |
| Aceptable | < 5% | Mantener programa y monitorear |

**Referencia industria maquiladora:** Sin programa de concientización, el promedio es del 22% al 35% en plantas manufactureras.

#### Security Awareness Coverage

```
Cobertura = (Empleados capacitados / Total de empleados) × 100
```

**Meta recomendada para maquiladoras:** ≥ 90%
Incluir: operadores de línea, supervisores, staff administrativo, ingeniería

---

## Laboratorio 1 — Análisis de phishing con TryHackMe

**Duración:** 1 hora
**Plataforma:** TryHackMe — Módulo "Phishing Analysis"

### Objetivo
Identificar correos de phishing usando técnicas de análisis de cabeceras, dominios y contenido.

### Instrucciones

1. Acceder a TryHackMe: [https://tryhackme.com](https://tryhackme.com)
2. Buscar la sala: **"Phishing Emails in Action"** o **"Phishing Analysis Tools"**
3. Completar los ejercicios de análisis de cabeceras de correo

### Ejercicios del laboratorio

**Ejercicio 1 — Análisis de cabeceras**

Dado el siguiente extracto de cabecera de correo, identificar anomalías:

```
From: rrhh@lear.com.mx-notificaciones.net
Reply-To: pagos.urgentes@gmail.com
X-Originating-IP: 185.220.101.45
Received: from mail.bulkmailer.ru
Subject: Actualización urgente de datos bancarios — Nómina Abril
```

**Preguntas:**
- ¿Cuál es el dominio real del remitente?
- ¿Por qué el Reply-To es diferente al From?
- ¿Qué indica la IP de origen `185.220.101.45`?
- ¿Por qué `mail.bulkmailer.ru` es una señal de alerta?

**Ejercicio 2 — Verificación de dominio**

Usar herramientas online para analizar dominios sospechosos:
- [https://mxtoolbox.com](https://mxtoolbox.com) — Verificar registros MX, SPF, DMARC
- [https://whois.domaintools.com](https://whois.domaintools.com) — Ver fecha de registro del dominio

Dominios a analizar (simulados):
- `lear-corporation-mx.com`
- `foxconn-pagos.net`
- `bosch-proveedores.mx`

**Preguntas:**
- ¿Cuándo fue registrado cada dominio?
- ¿Tienen registros DMARC configurados?
- ¿El dominio tiene reputación maliciosa?

### Resultado esperado
Identificación correcta del **80% de los correos maliciosos** presentados.

---

## Laboratorio 2 — Detección de deepfakes

**Duración:** 45 minutos

### Objetivo
Desarrollar la habilidad de identificar audio y video manipulado con IA.

### Materiales
El instructor presentará ejemplos de:
- Audios clonados de voz (generados con ElevenLabs para el ejercicio)
- Videos con rostros manipulados
- Videollamadas simuladas con deepfake

### Lista de verificación — Señales de deepfake

**En audio:**
- [ ] ¿Hay artefactos o distorsiones inusuales en la voz?
- [ ] ¿El tono emocional corresponde al contexto del mensaje?
- [ ] ¿Hay ruido de fondo artificial o ausente de forma sospechosa?
- [ ] ¿La persona evita responder preguntas específicas o espontáneas?

**En video:**
- [ ] ¿Los bordes del cabello y cuello se ven difusos o pixelados?
- [ ] ¿La persona parpadea de forma natural (15–20 veces por minuto)?
- [ ] ¿Las sombras del rostro corresponden a la iluminación del fondo?
- [ ] ¿El movimiento de labios está sincronizado con el audio?
- [ ] ¿Hay inconsistencias cuando la persona gira o inclina la cabeza?

### Protocolo de verificación ante videollamada sospechosa

1. Pedir a la persona que mueva la cabeza de lado a lado lentamente
2. Hacer una pregunta personal que solo la persona real podría responder
3. Solicitar continuar la llamada por teléfono (línea diferente)
4. Verificar con un colega si la persona realmente realizó la llamada

---

## Ejercicio práctico — Simulación BEC en planta de Juárez

**Duración:** 1 hora

### Escenario

**Empresa ficticia:** Electrocomponentes del Norte S.A. de C.V. — Planta de manufactura de arneses eléctricos en el Parque Industrial FINSA, Ciudad Juárez.

**Correo recibido por el Jefe de Cuentas por Pagar:**

---

> **De:** director.operaciones@electrocomponentes-norte.com.operaciones-mx.net
> **Para:** cuentas.pagar@electrocomponentes-norte.com
> **Asunto:** RE: Pago urgente — Proveedor estratégico — CONFIDENCIAL
>
> Gabriela,
>
> Por instrucciones del Sr. Ramírez (CEO, Dallas) necesitamos realizar un pago de emergencia de **$83,500 USD** a nuestro proveedor de cobre Metálicos del Pacífico S.A. El retraso puede parar la línea de producción del cliente Delphi mañana por la mañana.
>
> El proveedor cambió sus datos bancarios la semana pasada. Los nuevos datos son:
> - Banco: BBVA México
> - CLABE: 012180015123456785
> - Beneficiario: Metálicos del Pacífico Holding LLC
>
> Es urgente procesarlo antes de las 3 PM de hoy. No menciones esto al equipo de compras aún, están en auditoría y no quiero distraerlos.
>
> Gracias,
> **Ing. Roberto Vega**
> Director de Operaciones

---

### Actividades del equipo

**Parte 1 — Análisis del correo (15 minutos)**

Identificar todas las señales de alerta en el correo:
1. Analizar el dominio del remitente
2. Listar las técnicas de ingeniería social utilizadas
3. Clasificar el tipo de ataque según MITRE ATT&CK

**Parte 2 — Protocolo de verificación (15 minutos)**

Diseñar el proceso de verificación que Gabriela debe seguir:
1. ¿A quién contactar para verificar?
2. ¿Por qué medio (no por el mismo correo)?
3. ¿Qué preguntas hacer?
4. ¿Qué documentación solicitar?

**Parte 3 — Propuesta de control (30 minutos)**

Diseñar un **protocolo de transferencias** para la planta que incluya:
- Umbral a partir del cual se requiere doble autorización
- Proceso de verificación de cambios de cuenta bancaria de proveedores
- Canales de comunicación autorizados para transferencias urgentes
- Tiempo máximo de respuesta antes de escalar

### Métricas evaluadas
- Número de señales de alerta identificadas (meta: ≥ 8 de 10)
- Calidad del protocolo de verificación propuesto
- Tiempo de análisis del correo

---

## Resumen del día 1

| Elemento | Detalle |
|----------|---------|
| Amenazas cubiertas | Phishing con IA, BEC, deepfakes, ataques a cadena de suministro |
| Estándares aplicados | MITRE ATT&CK (TA0001, TA0006, TA0043), CIS Controls 5, 9, 14 |
| Plataformas usadas | TryHackMe |
| Métricas aprendidas | Phishing Click Rate, Security Awareness Coverage |
| Contexto local | Maquiladoras de Juárez, proveedores locales, ERP corporativos |

---

*Siguiente sesión → Día 2: Gestión de Identidad y Arquitectura Zero Trust*
