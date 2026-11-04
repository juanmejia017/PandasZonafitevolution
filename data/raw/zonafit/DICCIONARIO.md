# Base de datos simulada de Zona Fit Evolution

> **Estos datos son ficticios.** Zona Fit Evolution todavía no tiene datos reales de operación, así que estos archivos imitan una exportación de la base de datos MySQL del gimnasio.
>
> - No hay datos personales: no hay nombres, teléfonos ni correos, y el documento de identidad aparece como un código anonimizado.
> - Para que el diagnóstico de calidad sea realista, se introdujeron a propósito problemas típicos de un sistema en producción. Identificarlos es parte del trabajo de diagnóstico.

**Periodo cubierto:** del 1 de enero de 2025 al 15 de octubre de 2026 (fecha de corte de la exportación).

## Tablas y relaciones

```
planes (id_plan) ──< membresias (id_plan)
miembros (id_miembro) ──< membresias (id_miembro)
miembros (id_miembro) ──< accesos (id_miembro)
membresias (id_membresia) ──< pagos (id_membresia)
```

## `planes.csv`: catálogo de planes

| Columna | Descripción |
|---|---|
| `id_plan` | Identificador del plan |
| `nombre_plan` | Nombre comercial del plan |
| `tipo_plan` | `Ilimitado` (ingresos sin límite durante la vigencia) o `Tiquetera` (número fijo de ingresos) |
| `duracion_dias` | Días de vigencia del plan |
| `ingresos_incluidos` | Número de ingresos de la tiquetera; vacío en los planes ilimitados |
| `precio` | Precio de lista en pesos colombianos (COP) |

## `miembros.csv`: personas inscritas

| Columna | Descripción |
|---|---|
| `id_miembro` | Identificador del miembro |
| `documento_hash` | Documento de identidad anonimizado |
| `genero` | Género registrado en la inscripción |
| `fecha_nacimiento` | Fecha de nacimiento (AAAA-MM-DD) |
| `comuna` | Comuna de Medellín donde vive el miembro |
| `canal_captacion` | Cómo llegó al gimnasio: Instagram, Referido, Walk-in, Volante o Convenio empresarial |
| `fecha_registro` | Fecha de inscripción (AAAA-MM-DD) |

## `membresias.csv`: periodos de membresía comprados

Regla de negocio: los miembros no se eliminan. Cada compra o renovación crea una membresía nueva, y cuando pasa la fecha de fin la membresía debe quedar en estado `Vencida`.

| Columna | Descripción |
|---|---|
| `id_membresia` | Identificador de la membresía |
| `id_miembro` | Miembro que compró la membresía |
| `id_plan` | Plan comprado |
| `fecha_inicio` | Primer día de vigencia (AAAA-MM-DD) |
| `fecha_fin` | Último día de vigencia (AAAA-MM-DD) |
| `precio_pagado` | Valor cobrado en COP; puede tener descuento frente al precio de lista |
| `estado` | `Activa`, `Vencida` o `Cancelada` |

## `pagos.csv`: pagos de las membresías

| Columna | Descripción |
|---|---|
| `id_pago` | Identificador del pago |
| `id_membresia` | Membresía a la que corresponde el pago |
| `fecha_pago` | Fecha del pago |
| `valor` | Valor pagado en COP. Las membresías costosas pueden pagarse en dos cuotas |
| `metodo_pago` | Efectivo, Tarjeta, Transferencia o Nequi |
| `estado_pago` | `Aprobado`, `Pendiente` o `Rechazado` |

## `accesos.csv`: registros del lector de huella

Regla de negocio: el lector de huella abre la puerta solo si el miembro tiene una membresía activa. Solo se registra la entrada; la salida no queda registrada. La sede abre de 5:00 a 22:00.

| Columna | Descripción |
|---|---|
| `id_acceso` | Identificador del registro |
| `id_miembro` | Miembro identificado por la huella |
| `fecha_hora` | Fecha y hora del intento de ingreso (AAAA-MM-DD HH:MM:SS) |
| `resultado` | `Permitido` (la puerta abrió) o `Denegado` (no tenía membresía activa) |
| `dispositivo` | Lector que registró el intento |
