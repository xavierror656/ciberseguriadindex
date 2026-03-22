# Día 3 — Seguridad de Datos, Nube y Trabajo Híbrido

**Duración:** 4 horas
**Fecha:** Miércoles 26 de marzo de 2026

---

## Objetivo del día

Proteger la información de las plantas manufactureras de Ciudad Juárez en escenarios de trabajo híbrido: uso seguro de la nube, dispositivos personales en entornos laborales (BYOD), trabajo remoto con VPN, y cumplimiento de normativas de privacidad de datos.

---

## Bloque 1 — Seguridad en entornos de trabajo híbrido

**Duración:** 1 hora

### El trabajo híbrido en maquiladoras de Juárez

Las plantas manufactureras de Ciudad Juárez operan hoy en un modelo mixto: operadores en línea, ingenieros en planta, y personal administrativo que trabaja desde casa o desde múltiples sitios. Esta combinación crea nuevas superficies de ataque.

**Personal que trabaja de forma remota o híbrida:**
- Ingenieros de calidad que acceden a documentación técnica desde laptops personales
- Gerentes que revisan SAP y aprueban órdenes desde sus celulares
- Compradores que autorizan transferencias desde casa vía VPN
- Supervisores que consultan reportes de producción fuera de la planta

**Dispositivos no gestionados en uso laboral:**

| Situación | Riesgo | Frecuencia en planta |
|-----------|--------|----------------------|
| Celular personal para correo corporativo | Datos corporativos sin cifrado ni control remoto | Muy alta |
| Laptop personal conectada a VPN | Sin antivirus actualizado, sin parches de seguridad | Alta |
| Tablet personal con acceso a SharePoint | Archivos corporativos sincronizados sin MDM | Media |
| USB personal en equipo de planta | Posible introducción de malware | Media |

**El problema:** Cuando un empleado usa su dispositivo personal para trabajar, IT pierde la capacidad de aplicar controles, actualizar software o borrar datos corporativos de forma remota.

---

### Amenazas específicas a datos industriales en Juárez

#### Robo de propiedad intelectual

Las maquiladoras almacenan información de altísimo valor:

| Tipo de dato | Ejemplo en planta de Juárez | Valor para atacante |
|-------------|---------------------------|---------------------|
| Diseños de producto | Planos de arneses para Ford F-150 | Venta a competencia asiática |
| Procesos de manufactura | Parámetros de soldadura para iPhone | Replicación de proceso |
| Listas de materiales (BOM) | Componentes para dispositivos médicos | Espionaje industrial |
| Datos de clientes | Forecast de producción de Delphi | Información estratégica |
| Especificaciones de calidad | Tolerancias de piezas aeroespaciales | Falsificación de componentes |

#### Exfiltración de datos — Métodos más comunes en planta

1. **USB no autorizado** — Operador saca diseños en USB personal
2. **Email personal** — Empleado se reenvía archivos a Gmail o Hotmail
3. **Servicios de nube personal** — Subir archivos a Google Drive o Dropbox personales
4. **Impresión no controlada** — Imprimir documentos técnicos y sacarlos físicamente
5. **Fotografías con teléfono** — Fotografiar pantallas con diseños o datos de sistema

---

### Seguridad en la nube para maquiladoras

La mayoría de plantas en Juárez usan **Microsoft 365** (OneDrive, SharePoint, Teams) y SAP en nube. Las configuraciones incorrectas son la principal causa de fuga de datos.

#### Errores de configuración más comunes en SharePoint/OneDrive

**Error 1 — Carpetas compartidas públicamente por accidente**
```
Situación: Ingeniero comparte carpeta de diseños con "Cualquiera con el enlace"
           para enviársela a un proveedor
Resultado: El enlace queda accesible en internet sin autenticación
Datos expuestos: Especificaciones técnicas confidenciales del cliente
```

**Error 2 — Permisos heredados excesivos**
```
Situación: Carpeta de RRHH hereda permisos de la carpeta padre "Corporativo"
           a la que tienen acceso 400 empleados
Resultado: Todos los empleados pueden ver nóminas y expedientes
```

**Error 3 — Sincronización en dispositivos personales**
```
Situación: Gerente sincroniza OneDrive corporativo en su laptop personal
           sin cifrado ni MDM
Resultado: Al robar o perder la laptop, los datos quedan expuestos
```

---

### Seguridad de endpoints y política BYOD

**BYOD (Bring Your Own Device)** — Uso de dispositivos personales para trabajo corporativo.

**Riesgos principales del BYOD en maquiladoras:**

1. **Sin cifrado de disco** — Si se pierde el dispositivo personal, los datos corporativos quedan expuestos
2. **Mezcla de datos** — Fotos personales y archivos confidenciales en el mismo dispositivo
3. **Apps maliciosas** — Una app descargada puede acceder a archivos de trabajo sincronizados
4. **Sin gestión remota** — IT no puede borrar datos corporativos si el empleado es dado de baja
5. **Red doméstica insegura** — Router sin contraseña o con firmware desactualizado

**Controles para trabajo remoto seguro:**

| Control | Descripción | Costo |
|---------|-------------|-------|
| VPN corporativa | Túnel cifrado para todo el tráfico remoto | Incluido en la mayoría de firewalls |
| MDM (Mobile Device Management) | Gestión, políticas y borrado remoto de dispositivos | Microsoft Intune (incluido en M365 E3) |
| Conditional Access | Bloquear acceso desde dispositivos no gestionados | Azure AD Premium |
| Separación de perfiles | Contenedor corporativo separado del perfil personal | Microsoft Intune MAM |
| MFA obligatoria | Siempre requerida para acceso remoto | Incluido en M365 |

**Caso real adaptado a Juárez:**

> Un gerente de compras de una planta automotriz perdió su celular personal. Contenía correos con especificaciones técnicas confidenciales del cliente y datos bancarios de 40 proveedores. No fue posible hacer borrado remoto porque el dispositivo no estaba registrado en MDM.
>
> **Costo del incidente:** Notificación a 40 proveedores, revisión de contratos, auditoría interna, riesgo de incumplimiento LFPDPPP.

**Protocolo mínimo para BYOD en planta:**
1. Registrar el dispositivo personal en MDM antes de activar acceso a correo/SharePoint
2. Requerir PIN o biometría en el dispositivo
3. Permitir borrado remoto del perfil corporativo (no del dispositivo completo)
4. Revocar acceso y borrar datos corporativos el día de la baja del empleado

---

### Estándares aplicados

#### LFPDPPP — Ley Federal de Protección de Datos Personales en Posesión de Particulares

Las maquiladoras en México manejan datos personales de empleados, proveedores y clientes. La LFPDPPP establece obligaciones legales que IT y RRHH deben conocer.

**Datos personales que maneja una maquiladora:**

| Categoría | Ejemplos | Nivel de sensibilidad |
|-----------|----------|-----------------------|
| Empleados | CURP, RFC, datos bancarios (CLABE), expediente médico | Alto — datos sensibles |
| Nómina | Salarios, deducciones, cuentas bancarias | Alto |
| Clientes corporativos | Contactos, especificaciones de producto | Medio |
| Proveedores | RFC, cuentas bancarias, contratos | Medio |
| Visitantes | Nombre, identificación, fotografía | Bajo–Medio |

**Principios clave de la LFPDPPP:**
- **Licitud:** Solo recolectar datos con base legal (contrato laboral, necesidad empresarial)
- **Finalidad:** No usar datos del empleado para fines distintos a los informados
- **Proporcionalidad:** No recolectar más datos de los necesarios
- **Seguridad:** Implementar medidas técnicas y organizativas para proteger los datos
- **Responsabilidad:** Nombrar un responsable interno de privacidad

**Obligaciones prácticas para maquiladoras:**
- Aviso de privacidad publicado y firmado por empleados al ingreso
- Proceso para atender derechos ARCO (Acceso, Rectificación, Cancelación, Oposición)
- Notificación al INAI en caso de brecha de seguridad que afecte datos personales
- Contratos de confidencialidad con proveedores que manejen datos de la empresa

#### CIS Critical Security Controls

| Control | Descripción | Aplicación en planta |
|---------|-------------|---------------------|
| **Control 3 — Data Management** | Inventario y protección de datos sensibles | Mapeo de dónde viven los datos de empleados y proveedores |
| **Control 13 — Network Monitoring** | Visibilidad del tráfico de datos | Detectar exfiltración vía correo personal o USB |

---

### Métricas de seguridad

#### Patch Compliance Rate

```
Patch Compliance = (Sistemas parcheados en tiempo / Total de sistemas críticos) × 100
```

**Meta:** 100% de parches críticos aplicados en ≤ 72 horas

**Realidad OT en maquiladoras:**
- Muchos PLC llevan 5–10 años sin actualizaciones por miedo a interrumpir producción
- Windows XP y Windows 7 aún en uso en estaciones HMI de plantas de Juárez
- Parches deben coordinarse con paradas de mantenimiento programadas

**Proceso recomendado para OT:**
1. Evaluar parche en ambiente de prueba (gemelo digital o sistema backup)
2. Coordinar con producción para ventana de mantenimiento
3. Aplicar en turno de menor producción (generalmente fin de semana)
4. Verificar funcionalidad antes de retomar producción

#### Asset Inventory Coverage

```
Inventario = (Activos identificados / Total estimado de activos) × 100
```

**Meta:** 100% — No puedes proteger lo que no conoces

**Herramienta gratuita:** Nmap para IT, Claroty o Dragos (versión demo) para OT

#### Data Exposure Index

```
DEI = Número de archivos/carpetas críticas con acceso público o excesivo
```

**Meta:** 0 archivos críticos con acceso público

---

## Laboratorio 5 — Seguridad Web con OWASP Juice Shop

**Duración:** 1 hora
**Plataforma:** OWASP Juice Shop

### Objetivo
Entender vulnerabilidades web que afectan a portales industriales: portales de proveedores, sistemas de calidad online, acceso remoto a MES.

### Instalación local (sin internet necesario)

```bash
# Con Docker (recomendado)
docker pull bkimminich/juice-shop
docker run -d -p 3000:3000 bkimminich/juice-shop
# Acceder en: http://localhost:3000
```

### Contexto industrial

**Los portales web industriales en Juárez más comunes:**
- Portal de proveedores para envío de facturas y documentación
- Sistema de calidad online para reportes de PPAP y 8D
- Portal de empleados para consulta de nómina y vacaciones
- Acceso remoto vía web a sistemas MES

Estos portales frecuentemente tienen las mismas vulnerabilidades que Juice Shop.

### Ejercicios del laboratorio

**Ejercicio 1 — SQL Injection (Nivel: Fácil)**

Objetivo: Acceder como administrador sin conocer la contraseña

```
En el campo de email del login, ingresar:
' OR 1=1--

Esto convierte la consulta SQL en:
SELECT * FROM users WHERE email='' OR 1=1--' AND password='...'
→ 1=1 siempre es verdadero → Acceso concedido
```

**Impacto real en portal de proveedores de maquiladora:**
- Acceder a información de todos los proveedores
- Ver facturas de otros proveedores
- Modificar datos de pago

**Prevención:** Usar consultas parametrizadas (prepared statements), nunca construir SQL con concatenación de strings

**Ejercicio 2 — XSS (Cross-Site Scripting)**

Objetivo: Ejecutar código JavaScript en el navegador de otro usuario

```javascript
// En el campo de comentario o búsqueda, ingresar:
<script>alert('XSS en portal de proveedores!')</script>
```

**Impacto real en maquiladora:**
- Robar cookies de sesión de empleados de compras
- Redirigir a página falsa de login para robar credenciales
- Ejecutar acciones en nombre del usuario sin que lo sepa

**Prevención:** Sanitizar y escapar toda entrada de usuario antes de mostrarla en HTML

**Ejercicio 3 — Manipulación de sesión**

Objetivo: Acceder a cuenta de otro usuario manipulando cookies o tokens

1. Hacer login con cuenta propia
2. Inspeccionar el token de sesión (F12 → Application → Cookies)
3. Decodificar el JWT en [https://jwt.io](https://jwt.io)
4. Analizar qué información contiene y si puede ser manipulado

**Impacto real:** Si el portal usa IDs predecibles, un atacante puede cambiar `user_id=1043` a `user_id=1044` y ver información de otro proveedor.

---

## Laboratorio 6 — Auditoría de configuración de nube

**Duración:** 1 hora

### Objetivo
Identificar configuraciones inseguras en servicios de nube similares a los usados en maquiladoras de Juárez.

### Escenario

**Empresa ficticia:** Precision Medical Juárez S.A. de C.V. — Fabricante de instrumental médico para exportación a EE. UU.

El equipo de IT configuró Microsoft 365 hace 2 años sin seguir mejores prácticas. Se detectó que documentación técnica confidencial fue descargada desde IPs de China.

### Lista de verificación — Auditoría de Microsoft 365

**SharePoint / OneDrive:**
- [ ] ¿Hay carpetas o sitios compartidos con "Cualquiera con el enlace"?
- [ ] ¿Se puede compartir archivos fuera de la organización?
- [ ] ¿Los dispositivos personales pueden sincronizar OneDrive corporativo?
- [ ] ¿Hay política de retención y eliminación de datos?

**Exchange / Correo:**
- [ ] ¿Está habilitado el reenvío automático de correo a cuentas externas?
- [ ] ¿Se registran todos los correos enviados y recibidos?
- [ ] ¿Hay reglas de transporte que filtren información sensible?
- [ ] ¿Está configurado DMARC, DKIM y SPF en el dominio?

**Azure Active Directory:**
- [ ] ¿Hay cuentas de invitado (guest) activas sin uso reciente?
- [ ] ¿Las aplicaciones de terceros tienen permisos excesivos?
- [ ] ¿Está habilitado Conditional Access para bloquear países de alto riesgo?
- [ ] ¿Se revisan los reportes de risky sign-ins?

### Hallazgos típicos en maquiladoras de Juárez

| Hallazgo | Riesgo | Corrección |
|----------|--------|-----------|
| 47 carpetas con enlace público | Alto | Auditar y revocar enlaces públicos |
| Reenvío automático de correo del CFO a Gmail | Crítico | Deshabilitar y activar alerta |
| 23 cuentas de invitado sin uso en 180 días | Medio | Eliminar cuentas inactivas |
| 3 apps con permiso "Leer todos los archivos" | Alto | Revocar permisos excesivos |
| Sin Conditional Access configurado | Alto | Bloquear acceso desde países de riesgo |

---

## Ejercicio práctico — Diseño de política BYOD y análisis de privacidad

**Duración:** 1 hora

### Escenario

**Empresa ficticia:** Precision Electronics Juárez S.A. de C.V.
**Giro:** Manufactura de módulos electrónicos para la industria automotriz
**Empleados:** 350 (200 en producción, 100 en ingeniería y calidad, 50 en administración)
**Situación actual:** No existe política formal de BYOD. El 70% del personal administrativo usa su celular personal para correo corporativo y acceso a SharePoint.

**Incidente reciente:** Un gerente de compras perdió su celular personal. Contenía correos con especificaciones técnicas confidenciales del cliente y datos bancarios de 40 proveedores. No fue posible hacer borrado remoto porque el dispositivo no estaba en MDM.

### Actividades

**Parte 1 — Inventario de exposición actual (15 minutos)**

El equipo identifica:
1. ¿Qué sistemas corporativos son accesibles desde dispositivos personales actualmente?
2. ¿Qué datos pueden sincronizarse en dispositivos no gestionados?
3. ¿Qué procesos de trabajo remoto existen sin controles de seguridad?

**Parte 2 — Diseño de política BYOD (25 minutos)**

Los equipos definen los elementos clave de una política BYOD para la empresa:

| Elemento | Decisión del equipo | Justificación |
|----------|---------------------|---------------|
| ¿Se permite BYOD para correo corporativo? | Sí / No / Con condiciones | |
| ¿Se permite BYOD para SharePoint/documentos? | Sí / No / Con condiciones | |
| ¿Qué datos NO pueden estar en dispositivos personales? | | |
| ¿Se requiere MDM para acceso BYOD? | Sí / No | |
| ¿Qué ocurre con los datos al dar de baja al empleado? | | |
| ¿VPN obligatoria para trabajo remoto? | Sí / No | |
| ¿Qué pasa si el empleado no acepta MDM? | | |

**Parte 3 — Análisis de privacidad bajo LFPDPPP (20 minutos)**

Aplicando la Ley Federal de Protección de Datos Personales:

1. ¿La empresa tiene aviso de privacidad actualizado para empleados que cubra el uso de MDM?
2. ¿Se debe notificar a los 40 proveedores afectados por la pérdida del celular?
3. ¿Qué obligación tiene la empresa ante el INAI por este incidente?
4. ¿Qué medidas técnicas hubieran reducido el impacto del incidente?

### Métricas evaluadas

- Completitud y aplicabilidad de la política BYOD propuesta
- Identificación correcta de datos personales sensibles bajo LFPDPPP
- Calidad de controles técnicos propuestos (equilibrio seguridad vs. productividad)
- Consideración del impacto en empleados

---

## Resumen del día 3

| Elemento | Detalle |
|----------|---------|
| Temas cubiertos | Trabajo híbrido, BYOD, seguridad en nube, privacidad de datos |
| Estándares aplicados | LFPDPPP, mejores prácticas M365, CIS Controls 3 y 13 |
| Plataformas usadas | OWASP Juice Shop |
| Métricas aprendidas | Patch Compliance Rate, Asset Inventory Coverage, Data Exposure Index |
| Contexto local | Trabajo remoto en maquiladoras, datos de empleados y proveedores, INAI |

---

*Siguiente sesión → Día 4: Respuesta a Incidentes, Ransomware e Higiene Digital*
