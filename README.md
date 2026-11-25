# POO Fitness — Sistema de Gestión para Gimnasio (Entrega 1)

> **Asignatura:** Diseño y Programación Orientada a Objetos  
> **Estado:** Borrador — Entrega 1  
> **Dominio:** Gimnasio *"POO Fitness"* (Coatzacoalcos, Veracruz)

---

## 1. Investigación y Reglas del Negocio

### 1.1 Descripción del Dominio

**POO Fitness** es un establecimiento deportivo ubicado en Coatzacoalcos con una sola sucursal. Ofrece a sus socios acceso a áreas de entrenamiento (zona de pesas y cardio), clases grupales (**yoga** y **zumba**) y planes de entrenamiento personalizado.

#### Horario de Atención
* **Entre semana:** 07:00 a 22:00 hrs.
* **Fines de semana y días festivos:** 08:00 a 15:00 hrs.

#### Procesos Principales
1. **Registro de socios:** inscripción de una persona, registro de sus datos y asignación de una membresía.
2. **Gestión de membresías:** contratación, pago, renovación o vencimiento según su duración (**semanal**, **mensual** o **anual**).
3. **Gestión de visitas:** pago de acceso diario y registro de datos del visitante.
4. **Gestión de ventas:** cobro y registro de bebidas energéticas vendidas a un socio o visitante.
5. **Control de acceso:** verificación de membresía vigente (socio) o visita pagada en el día (visitante), mostrando identidad y autorización de ingreso.
6. **Gestión de clases grupales:** programación de clases con horario e instructor, e inscripción de socios.
7. **Entrenamiento personalizado:** asignación de un entrenador a un socio y seguimiento a su plan de ejercicios.
8. **Administración del personal:** alta y asignación de entrenadores y recepcionistas.
9. **Gestión de promociones:** aplicación de descuento del **25%** en la membresía seleccionada si el socio presenta credencial de estudiante vigente.

#### Alcance del Sistema
* **Incluido:** socios, membresías, visitas, horario de atención, venta de bebidas energéticas y su *stock*, pagos, promociones, entrenamiento personalizado, clases grupales, entrenadores, recepcionistas y dueño.
* **Excluido:** nómina y control de equipo o mantenimiento.

---

### 1.2 Roles

#### Visitantes y Socios
* **Visitante:** accede por un día previo pago de visita, registra sus datos con el recepcionista y puede comprar bebidas.
* **Socio:** accede según su membresía vigente, asiste a clases grupales, puede tener un entrenador personalizado y compra bebidas. Si es estudiante con credencial vigente, puede obtener descuento en su membresía.

#### Personal
* **Recepcionista:** atiende la entrada; registra socios y visitantes; cobra membresías, visitas y ventas; controla el acceso; verifica credencial de estudiante y aplica el descuento; e informa el horario de atención. Es el usuario principal del sistema.
* **Entrenador:** da seguimiento al plan de ejercicios de los socios asignados y puede impartir clases grupales (yoga, zumba).
* **Dueño:** administra al personal mediante el alta y asignación de entrenadores y recepcionistas.

---

### 1.3 Reglas de Negocio

#### Acceso y Membresías
* **RN-01:** Un socio solo puede entrar al gimnasio si su membresía está vigente.
* **RN-02:** Existen distintos tipos de membresía (semanal, mensual y anual), cada una con precio y beneficios distintos.
* **RN-03:** El visitante solo puede acceder el día en que pagó su visita, y sus datos deben registrarse antes de entrar.
* **RN-04:** Un socio solo puede tener una membresía vigente a la vez.

#### Clases y Entrenamiento
* **RN-05:** Una clase grupal tiene horario de inicio y fin.
* **RN-06:** Una clase grupal solo puede ser impartida por un entrenador, y solo los socios pueden asistir a ella.
* **RN-07:** Un entrenador puede atender a varios socios, pero cada socio tiene un solo entrenador personalizado a la vez.

#### Ventas y Personal
* **RN-08:** Una bebida solo puede venderse si hay existencias, y cada venta descuenta una unidad del *stock*.
* **RN-09:** Solo el dueño puede dar de alta y asignar al personal (entrenadores y recepcionistas).

#### Promoción
* **RN-10:** Un socio que sea estudiante y presente su credencial de estudiante vigente recibe un descuento del **25%** en la membresía que seleccione.

---

## 2. Requisitos Funcionales

| ID | Módulo | Descripción |
| :--- | :--- | :--- |
| **RF-01** | Clientes | Dar de alta a socios y visitantes registrando nombre, teléfono y fecha de registro. |
| **RF-02** | Clientes | Consultar, actualizar y dar de baja a un socio. |
| **RF-03** | Membresías y visitas | Registrar membresía (semanal, mensual o anual) y su pago, consultar vigencia y renovar calculando precio y fecha de vencimiento según tipo. |
| **RF-04** | Membresías y visitas | Registrar la visita de un visitante junto con su pago y consultar las visitas registradas. |
| **RF-05** | Acceso | Verificar acceso de socio o visitante mostrando identidad y si se concede el ingreso según membresía vigente o visita pagada hoy. |
| **RF-06** | Personal | Permitir al dueño dar de alta, consultar, actualizar y dar de baja a entrenadores y recepcionistas. |
| **RF-07** | Clases y entrenamiento | Crear, consultar, modificar y cancelar clases grupales (yoga, zumba) con horario inicio/fin, asignar entrenador e inscribir socios. |
| **RF-08** | Clases y entrenamiento | Asignar un entrenador a un socio y crear, consultar y actualizar su plan de ejercicios. |
| **RF-09** | Ventas | Registrar bebidas energéticas y existencias, registrar venta a socio o visitante descontando *stock* y consultar *stock* disponible. |
| **RF-10** | Promoción | Aplicar descuento de estudiante (25%) a la membresía seleccionada con credencial vigente, mostrando precio original y precio con descuento. |
| **RF-11** | Horario | Consultar el horario de atención (entre semana 07:00–22:00; fines de semana y festivos 08:00–15:00). |

### Justificación de Herencia y Polimorfismo en Java

* **Herencia (`extends`):**
    * `Persona` (clase abstracta base) → `Cliente` (abstracta) → `Socio` y `Visitante` (**RF-01**).
    * `Persona` → `Empleado` (abstracta) → `Recepcionista` y `Entrenador` (**RF-06**).
    * `Promocion` (clase abstracta) → `DescuentoEstudiante` (**RF-10**). *Nota:* `Promocion` es abstracta para permitir nuevas promociones futuras (p. ej., por membresía anual o cumpleaños) sin modificar `Membresia`.
* **Polimorfismo:**
    * Cálculo de precio y vigencia según el tipo de membresía (**RF-03**).
    * Verificación de acceso según si el cliente es `Socio` o `Visitante` (**RF-05**).
    * Cálculo del descuento según el tipo de `Promocion` (**RF-10**).

---

## 3. Diagrama de clases UML

Diseño orientado a objetos del sistema de gestión del gimnasio **POO Fitness**, una sucursal en Coatzacoalcos que ofrece membresías, visitas, clases grupales, entrenamiento personalizado y venta de bebidas energéticas.

El diagrama incluye:

- Clases con sus atributos y métodos, con su visibilidad (`+`, `-`).
- Multiplicidades y nombres de rol en cada relación.
- Herencia, composición, agregación, asociación y dependencia.
- Clases abstractas y enumeraciones.
- Organización por paquetes: personas, membresías, promociones, pagos, ventas, actividades, gestión y aplicación.

[Abrir el diagrama en draw.io](https://drive.google.com/file/d/11yYcB7iNocIEuEZnxSGLyT9GkanOZV43/view?usp=sharing)

El enlace abre la versión más reciente del archivo almacenado en Google Drive.

---

## Entrega 2. Modelado y fundamentos técnicos

### 2.1 Estructura de packages

```
poofitness/                      <- nombre del proyecto
└── src/
└── poofitness/              <- package raíz
├── app/
│   ├── Main.java
│   └── MenuConsola.java
└── modelo/
├── personas/
│   ├── Persona.java          (abstract)
│   ├── Cliente.java          (abstract)
│   ├── Empleado.java         (abstract)
│   ├── Socio.java
│   ├── Visitante.java
│   ├── Dueno.java
│   ├── Entrenador.java
│   └── Recepcionista.java
├── membresias/
│   ├── Membresia.java        (abstract)
│   ├── MembresiaSemanal.java
│   ├── MembresiaMensual.java
│   └── MembresiaAnual.java
├── promociones/
│   ├── Promocion.java        (abstract)
│   └── DescuentoEstudiante.java
├── pagos/
│   ├── Pago.java
│   └── Visita.java
├── acceso/
│   ├── ResultadoAcceso.java
│   └── HorarioAtencion.java
├── actividades/
│   ├── ClaseGrupal.java
│   ├── TipoClase.java        (enum)
│   ├── EstadoClase.java      (enum)
│   └── PlanEjercicios.java
├── ventas/
│   ├── Bebida.java
│   └── Venta.java
└── gestion/
└── Gimnasio.java
```
=======
## 3. Diagrama de clases UML

Diseño orientado a objetos del sistema de gestión del gimnasio **POO Fitness**, una sucursal en Coatzacoalcos que ofrece membresías, visitas, clases grupales, entrenamiento personalizado y venta de bebidas energéticas.

El diagrama incluye:

- Clases con sus atributos y métodos, con su visibilidad (`+`, `-`).
- Multiplicidades y nombres de rol en cada relación.
- Herencia, composición, agregación, asociación y dependencia.
- Clases abstractas y enumeraciones.
- Organización por paquetes: personas, membresías, promociones, pagos, ventas, actividades, gestión y aplicación.

[Abrir el diagrama en draw.io](https://drive.google.com/file/d/11yYcB7iNocIEuEZnxSGLyT9GkanOZV43/view?usp=sharing)

El enlace abre la versión más reciente del archivo almacenado en Google Drive.
>>>>>>> f8f692c2ae9bd76ef6d788033d2c4e1ab613de57
