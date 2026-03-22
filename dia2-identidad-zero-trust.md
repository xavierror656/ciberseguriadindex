# Día 2 — Gestión de Identidad y Arquitectura Zero Trust

**Duración:** 4 horas
**Fecha:** Martes 25 de marzo de 2026

---

## Objetivo del día

Aprender a proteger el acceso a sistemas críticos de plantas manufactureras mediante gestión de identidades, autenticación multifactor y principios de Zero Trust aplicados al entorno industrial de Ciudad Juárez.

---

## Bloque 1 — Control de accesos en entornos industriales

**Duración:** 1 hora

### El problema de accesos en maquiladoras de Juárez

Las plantas manufactureras de Ciudad Juárez enfrentan desafíos únicos de gestión de identidad:

**Alta rotación de personal**
- Rotación anual del 40%–80% en operadores de producción
- Cuentas de exempleados que permanecen activas semanas después de su salida
- Cambios frecuentes de turno y posición que no se reflejan en permisos de sistema

**Acceso multisistema complejo**

| Sistema | Usuarios típicos | Riesgo si se compromete |
|---------|-----------------|------------------------|
| SAP / Oracle ERP | Finanzas, Compras, RRHH | Fraude financiero, fuga de datos |
| MES (Manufacturing Execution System) | Ingeniería, Producción | Manipulación de órdenes de fabricación |
| Correo corporativo (Exchange/O365) | Todos | Phishing, BEC, exfiltración |
| VPN corporativa | IT, Ingeniería, Gerencia | Acceso remoto no autorizado a red |
| SCADA / HMI | Técnicos de mantenimiento | Sabotaje de línea de producción |
| Sistemas de nómina (Kronos, ADP) | RRHH, Finanzas | Fraude de nómina |

**Acceso de terceros sin control**
- Técnicos de mantenimiento de equipos (Fanuc, KUKA, ABB) con acceso temporal
- Auditores externos de clientes (Ford, GM, BMW) conectados a red interna
- Consultores de IT con credenciales permanentes después de terminar proyectos
- Proveedores de servicios gestionados (MSP) con acceso privilegiado

---

### Caso real adaptado — Robo de acceso a ERP en planta automotriz

**Escenario:** Planta de manufactura de asientos automotrices en Juárez (600 empleados)

**Cronología del ataque:**

```
Semana 1: Atacante envía correo de phishing al Coordinador de IT
          → El coordinador hace clic en enlace malicioso
          → Se instala keylogger silencioso en su equipo

Semana 2: Atacante obtiene credenciales de SAP del coordinador
          → Accede al módulo de Cuentas por Pagar
          → Estudia patrones de pagos y proveedores reales

Semana 3: Atacante modifica datos bancarios de proveedor legítimo en SAP
          → Cambia CLABE de Aceros Especiales del Norte S.A.
          → El siguiente pago de $120,000 USD se transfiere a cuenta mula

Semana 4: La empresa descubre el fraude al recibir llamada del proveedor
          real solicitando su pago pendiente
```

**Controles que hubieran prevenido el ataque:**
- MFA en cuenta de SAP del coordinador de IT ✓
- Alertas de cambio de datos bancarios en ERP ✓
- Segregación de funciones (quien modifica datos no puede autorizar pagos) ✓
- Revisión de acceso privilegiado trimestral ✓

---

### Autenticación multifactor en manufactura

#### Tipos de MFA y aplicación en planta

| Tipo de MFA | Ejemplo | Recomendado para |
|------------|---------|-----------------|
| Aplicación autenticadora | Microsoft Authenticator, Google Authenticator | Oficinas, Ingeniería |
| Token físico | YubiKey, RSA SecurID | Cuentas de administrador de IT |
| SMS (menos seguro) | Código por mensaje de texto | Usuarios generales como última opción |
| Biométrico | Huella dactilar, reconocimiento facial | Acceso físico a áreas restringidas |
| Tarjeta inteligente | Smart card + PIN | Acceso a sistemas SCADA críticos |

#### Desafíos de MFA en planta de producción

**Problema:** Operadores en línea de producción no tienen teléfono a la mano

**Soluciones:**
- Kioscos de acceso compartido con tarjeta + PIN para operadores
- MFA solo para sistemas administrativos y críticos, no para inicio de sesión en terminales de producción
- Tokens físicos para supervisores de turno

---

### Gestión de cuentas privilegiadas (PAM)

Las cuentas con privilegios de administrador son el objetivo principal de los atacantes.

**Inventario típico de cuentas privilegiadas en maquiladora:**
- Administradores de dominio (Active Directory)
- Administradores de SAP (BASIS)
- Root / Administrador local en servidores
- Cuentas de servicio de aplicaciones
- Administradores de firewall y switches
- Cuentas de acceso remoto de proveedores de equipos

**Regla del privilegio mínimo en manufactura:**

> Un ingeniero de calidad no necesita acceso de escritura al módulo financiero de SAP.
> Un técnico de mantenimiento no necesita acceso a la red de oficinas.
> Un usuario de nómina no necesita derechos de administrador local en su PC.

---

### Estándares aplicados

#### NIST Cybersecurity Framework

| Función | Actividad | Aplicación en planta |
|---------|-----------|---------------------|
| **Identify** | Inventario de activos y cuentas | Mapear todos los usuarios, sistemas y accesos en planta |
| **Protect** | Control de acceso | Implementar MFA, privilegio mínimo, revisión de accesos |

#### ISO 27001

| Control | Descripción | Implementación en maquiladora |
|---------|-------------|------------------------------|
| A.5 — Control de accesos | Política de acceso formal | Definir quién puede acceder a qué sistema y por qué |
| A.6 — Gestión de identidades | Registro y baja de usuarios | Proceso formal de onboarding/offboarding por RRHH+IT |
| A.9 — Acceso a sistemas | Revisión periódica de accesos | Auditoría trimestral de permisos activos |

---

### Métricas de seguridad — Bloque 2

#### MFA Coverage Rate

```
MFA Coverage = (Cuentas con MFA activo / Total de cuentas) × 100
```

| Tipo de cuenta | Meta | Justificación |
|---------------|------|---------------|
| Administradores de IT | 100% | Acceso total a infraestructura |
| Usuarios de ERP (SAP/Oracle) | 95% | Acceso a datos financieros y operativos |
| Acceso VPN | 100% | Punto de entrada a red interna |
| Usuarios de correo corporativo | 80% | Principal vector de ataque |
| Usuarios generales | 70% | Reducción de riesgo general |

#### Privileged Account Ratio

```
PAR = (Cuentas con privilegios administrativos / Total de cuentas) × 100
```

**Meta recomendada:** < 5%

**Ejemplo:** Si una planta tiene 500 usuarios en Active Directory, no debería haber más de 25 cuentas con privilegios de administrador.

#### Account Lifecycle Compliance

```
Compliance = (Cuentas desactivadas en ≤48h después de baja / Total de bajas) × 100
```

**Meta:** 100% — Cero cuentas activas de exempleados

**Realidad en maquiladoras sin proceso formal:** Cuentas que permanecen activas 30, 60, hasta 180 días después de la salida del empleado.

---

## Laboratorio 3 — Linux Security Game con OverTheWire Bandit

**Duración:** 1 hora
**Plataforma:** OverTheWire — Bandit

### Objetivo
Comprender cómo funcionan las credenciales, permisos de archivos y control de acceso en sistemas Linux, que son la base de servidores industriales.

### Acceso al laboratorio

```bash
# Conectarse al nivel 0
ssh bandit0@bandit.labs.overthewire.org -p 2220
# Contraseña inicial: bandit0
```

### Niveles objetivo para el curso

| Nivel | Habilidad practicada | Relevancia industrial |
|-------|---------------------|----------------------|
| Bandit 0–1 | Lectura de archivos, navegación | Acceso a logs de sistemas |
| Bandit 2–3 | Archivos ocultos, espacios en nombres | Archivos de configuración industrial |
| Bandit 4–5 | Tipos de archivo, búsqueda | Localizar archivos de configuración |
| Bandit 6–7 | Permisos de usuario y grupo | Gestión de accesos en servidores Linux |
| Bandit 8–9 | Búsqueda en texto, strings únicos | Análisis de logs de eventos |

### Ejercicios contextualizados

**Ejercicio — Permisos de archivos críticos**

En un servidor Linux de planta (MES, Historian, SCADA en Linux):

```bash
# Ver permisos de un archivo de configuración crítico
ls -la /etc/scada/config.ini

# Salida que indica problema:
-rw-rw-rw- 1 root root 2048 Mar 15 08:22 config.ini
# Todos los usuarios pueden leer Y escribir este archivo → RIESGO ALTO

# Corrección adecuada:
chmod 640 /etc/scada/config.ini
# Solo root puede leer y escribir, el grupo puede leer, nadie más
```

**Ejercicio — Identificar cuentas con privilegios excesivos**

```bash
# Listar usuarios con acceso sudo (administradores)
cat /etc/sudoers | grep -v "^#"

# Ver últimos accesos al sistema
last | head -20

# Ver intentos fallidos de login
grep "Failed password" /var/log/auth.log | tail -20
```

**Discusión:** ¿Qué cuentas en este servidor no deberían tener sudo?

---

## Laboratorio 4 — Simulación de ataque de credenciales

**Duración:** 1 hora

### Objetivo
Comprender cómo funcionan los ataques de credenciales para poder detectarlos y defenderse.

### Escenario

**Empresa:** Planta de manufactura de dispositivos médicos en Juárez (proveedor de Stryker y Medtronic)
**Situación:** Se detectó actividad inusual en el sistema de Active Directory a las 2:30 AM

### Parte 1 — Análisis del ataque (30 minutos)

**Extracto del log de Active Directory:**

```
[2026-03-15 02:31:15] FAILED LOGIN - User: jlopez - IP: 192.168.1.105
[2026-03-15 02:31:16] FAILED LOGIN - User: jlopez - IP: 192.168.1.105
[2026-03-15 02:31:17] FAILED LOGIN - User: jlopez - IP: 192.168.1.105
[2026-03-15 02:31:45] FAILED LOGIN - User: mgarcia - IP: 192.168.1.105
[2026-03-15 02:31:46] FAILED LOGIN - User: mgarcia - IP: 192.168.1.105
[2026-03-15 02:31:47] FAILED LOGIN - User: mgarcia - IP: 192.168.1.105
[2026-03-15 02:32:10] SUCCESS LOGIN - User: rherrera - IP: 192.168.1.105
[2026-03-15 02:32:12] ACCESS - User: rherrera - Resource: \\fileserver\Finanzas
[2026-03-15 02:32:15] ACCESS - User: rherrera - Resource: \\fileserver\RRHH
[2026-03-15 02:32:45] FILE DOWNLOAD - User: rherrera - File: nomina_2026_Q1.xlsx
[2026-03-15 02:33:01] FILE DOWNLOAD - User: rherrera - File: lista_empleados_completa.xlsx
```

**Preguntas de análisis:**
1. ¿Qué tipo de ataque está ocurriendo?
2. ¿A qué hora comenzó? ¿Por qué es significativo ese horario?
3. ¿Qué IP está realizando el ataque? ¿Es interna o externa?
4. ¿Qué cuenta fue comprometida exitosamente?
5. ¿Qué datos fueron robados?
6. ¿Qué controles habrían detenido este ataque?

### Parte 2 — Respuesta inmediata (15 minutos)

Definir las acciones a tomar en orden de prioridad:
- [ ] Deshabilitar la cuenta `rherrera` inmediatamente
- [ ] Bloquear la IP `192.168.1.105` en el firewall
- [ ] Notificar al responsable de ciberseguridad
- [ ] Iniciar investigación forense (no modificar evidencia)
- [ ] Notificar a RRHH sobre posible fuga de datos de empleados
- [ ] Revisar qué más accedió el atacante con esa cuenta

### Parte 3 — Controles de mitigación (15 minutos)

Proponer controles para prevenir este ataque en el futuro:

| Control | Implementación | Costo estimado |
|---------|---------------|----------------|
| Account Lockout Policy | Bloquear cuenta tras 5 intentos fallidos | Gratis (GPO en AD) |
| MFA en todas las cuentas | Microsoft Authenticator | Incluido en M365 |
| Alertas de login fuera de horario | SIEM o Azure AD | Variable |
| Restricción de horario de login | GPO — Solo de 6 AM a 10 PM | Gratis |
| Monitoreo de descarga masiva de archivos | DLP en SharePoint/OneDrive | Incluido en M365 E3 |

---

## Ejercicio de arquitectura — Zero Trust para planta industrial

**Duración:** 1 hora

### Concepto Zero Trust en manufactura

**Principio fundamental:** "Nunca confíes, siempre verifica"

En el modelo tradicional de una maquiladora:
- Si estás dentro de la red de la planta, se confía en ti automáticamente
- Un atacante que entra por VPN o phishing tiene acceso a todo

En Zero Trust:
- Cada acceso se verifica independientemente del origen
- Los sistemas no confían entre sí automáticamente
- El acceso se otorga solo para la tarea específica

### Actividad — Diseñar arquitectura Zero Trust

**Planta de referencia:** Fabricante de arneses eléctricos automotrices, 800 empleados, Juárez

**Activos a proteger y segmentar:**

```
ZONA 1 — Corporativa / Oficinas
├── ERP SAP (Finanzas, Compras, RRHH)
├── Correo corporativo (Office 365)
├── Servidores de archivos
└── Videoconferencia (Teams)

ZONA 2 — Ingeniería / Calidad
├── CAD/CAM (diseño de arneses)
├── Sistema de calidad (PLEX, Arena)
├── Documentación técnica
└── Estaciones de trabajo de ingenieros

ZONA 3 — Producción / OT
├── MES (Manufacturing Execution System)
├── Pruebas eléctricas automatizadas
├── Lectores de código de barras en línea
└── Pantallas HMI de producción

ZONA 4 — Acceso remoto / Terceros
├── VPN de técnicos de mantenimiento
├── Acceso auditores externos (cliente Ford)
└── Portal de proveedores
```

### Diseño esperado del equipo

Los equipos deberán definir:

**1. Segmentación de red**
- ¿Qué zonas pueden comunicarse entre sí?
- ¿Qué tipo de tráfico está permitido entre zonas?
- ¿Cómo se aísla la red de producción?

**2. Controles de acceso por zona**

| Zona | MFA requerido | Dispositivo permitido | Horario |
|------|--------------|----------------------|---------|
| Corporativa | Sí | Corporativo + personal | 24/7 |
| Ingeniería | Sí | Solo corporativo | Lunes–Sábado 6AM–10PM |
| Producción | No (tarjeta) | Solo terminales de planta | N/A |
| Acceso remoto | Sí + Justificación | Solo corporativo | Con ticket abierto |

**3. Monitoreo y detección**
- ¿Qué eventos deben generar alertas?
- ¿Quién responde a las alertas y en qué tiempo?

**4. Acceso de terceros**
- ¿Cómo se otorga acceso temporal a técnicos de Fanuc o ABB?
- ¿Qué pueden ver y qué no?
- ¿Cómo se revoca el acceso cuando termina el servicio?

### Métricas evaluadas

- Reducción de cuentas con privilegios excesivos
- Cobertura de MFA por tipo de cuenta
- Tiempo de desactivación de cuentas de exempleados
- Calidad de la segmentación propuesta

---

## Resumen del día 2

| Elemento | Detalle |
|----------|---------|
| Amenazas cubiertas | Robo de credenciales, cuentas privilegiadas, acceso no autorizado |
| Estándares aplicados | NIST CSF (Identify, Protect), ISO 27001 A.5/A.6/A.9 |
| Plataformas usadas | OverTheWire Bandit |
| Métricas aprendidas | MFA Coverage Rate, Privileged Account Ratio, Account Lifecycle Compliance |
| Contexto local | SAP en maquiladoras, rotación de personal, acceso de proveedores OEM |

---

*Siguiente sesión → Día 3: Seguridad de Datos, Nube y Redes Industriales*
