# Sistema Bancario

##  Descripción del proyecto

Este proyecto es un **sistema bancario** desarrollado con fines académicos, que simula las operaciones básicas de una entidad financiera. Permite a los clientes autenticarse, registrarse, abrir cuentas, realizar depósitos, retiros, transferencias, consultar su saldo, revisar su historial de transacciones y pagar servicios. Además, cuenta con un módulo de administración para la gestión de usuarios del sistema.

El proyecto fue desarrollado en pareja siguiendo la metodología **Git Flow**, dividiendo el trabajo en módulos independientes (features) para facilitar la colaboración, el control de versiones y la trazabilidad de los aportes de cada integrante.

**Objetivo del proyecto:** aplicar buenas prácticas de control de versiones (Git Flow), trabajo colaborativo en GitHub y desarrollo modular de software.

##  Enlace del repositorio

```
https://github.com/tu-usuario/banco-sistema
```

---

##  Instrucciones de ejecución

### Requisitos previos
- Git instalado
- [Node.js / Python / Java — ajustar según el stack real] instalado
- Gestor de paquetes correspondiente (npm, pip, maven, etc.)
- Base de datos configurada (ver `.env.example`)

### Pasos para ejecutar el proyecto

1. **Clonar el repositorio**
```bash
git clone https://github.com/tu-usuario/banco-sistema.git
cd banco-sistema
```

2. **Cambiar a la rama develop** (rama de desarrollo activo)
```bash
git checkout develop
```

3. **Instalar dependencias**
```bash
npm install
```

4. **Configurar variables de entorno**
```bash
cp .env.example .env
# Editar .env con las credenciales de tu base de datos
```

5. **Ejecutar el proyecto**
```bash
npm run dev
```

6. **Ejecutar las pruebas**
```bash
npm run test
```

La aplicación quedará disponible en `http://localhost:3000` (ajustar puerto según configuración real).

---

## 🌳 Estructura de ramas (Git Flow)

```
main
│
├── develop
│
├── feature/login
├── feature/registro-clientes
├── feature/apertura-cuentas
├── feature/depositos
├── feature/retiros
├── feature/transferencias
├── feature/consulta-saldo
├── feature/historial-transacciones
├── feature/pagos-servicios
├── feature/administracion-usuarios
│
├── release/v1.0.0
├── release/v1.1.0
│
├── hotfix/error-transferencias
└── hotfix/error-login
```

### Descripción de ramas

| Rama | Propósito |
|---|---|
| `main` | Código en producción. Siempre estable y desplegable. |
| `develop` | Integración de todas las features. Base para releases. |
| `feature/*` | Desarrollo de una funcionalidad específica. Sale de `develop` y regresa a `develop`. |
| `release/*` | Preparación de una nueva versión (ajustes finales, pruebas). Sale de `develop`, se fusiona a `main` y `develop`. |
| `hotfix/*` | Corrección urgente en producción. Sale de `main`, se fusiona a `main` y `develop`. |

---

##  Flujo de trabajo

### Crear una feature
```bash
git checkout develop
git pull origin develop
git checkout -b feature/nombre-feature
git push -u origin feature/nombre-feature
```

### Finalizar una feature
1. Hacer commit de los cambios (ver convención abajo).
2. Hacer push a la rama feature.
3. Abrir Pull Request hacia `develop`.
4. Esperar revisión (code review) de al menos 1 persona.
5. Al aprobarse, hacer merge y eliminar la rama feature.

### Crear un release
```bash
git checkout develop
git pull origin develop
git checkout -b release/vX.X.X
git push -u origin release/vX.X.X
```
Al finalizar pruebas:
```bash
git checkout main
git merge release/vX.X.X
git tag -a vX.X.X -m "Versión X.X.X"
git push origin main --tags

git checkout develop
git merge release/vX.X.X
git push origin develop
```

### Crear un hotfix
```bash
git checkout main
git checkout -b hotfix/nombre-error
# corregir el error
git checkout main
git merge hotfix/nombre-error
git tag -a vX.X.X -m "Fix: nombre-error"
git push origin main --tags

git checkout develop
git merge hotfix/nombre-error
git push origin develop
```

---

##  Convención de commits

Se recomienda seguir **Conventional Commits**:

```
tipo(módulo): descripción breve
```

**Tipos permitidos:**
- `feat`: nueva funcionalidad
- `fix`: corrección de bug
- `docs`: cambios en documentación
- `style`: formato, sin cambios de lógica
- `refactor`: refactorización de código
- `test`: agregar o corregir pruebas
- `chore`: tareas de mantenimiento (configuración, dependencias)

**Ejemplos:**
```
feat(login): agregar validación de intentos fallidos
fix(transferencias): corregir cálculo de saldo tras transferencia
docs(readme): actualizar estructura de ramas
test(depositos): agregar pruebas unitarias de depósito
```

---

##  Convención de Pull Requests

**Título del PR:**
```
[feature/módulo] Descripción breve del cambio
```
Ejemplo: `[feature/depositos] Implementar registro de depósitos`

**Descripción del PR debe incluir:**
- Qué se hizo
- Cómo probarlo
- Capturas de pantalla (si aplica)
- Checklist de revisión (ver abajo)

###  Checklist antes de solicitar revisión

- [ ] El código sigue las convenciones del proyecto
- [ ] Se agregaron/actualizaron pruebas unitarias
- [ ] Todas las pruebas pasan localmente
- [ ] No hay credenciales ni datos sensibles en el código
- [ ] La rama está actualizada con `develop`
- [ ] Se actualizó la documentación si es necesario

---

##  Módulos y funcionalidades

| Módulo | Descripción |
|---|---|
| **Login** | Autenticación de usuarios, manejo de sesión, bloqueo por intentos fallidos, recuperación de contraseña |
| **Registro de clientes** | Alta de clientes, validación de duplicados, verificación de datos básicos (KYC) |
| **Apertura de cuentas** | Creación de cuentas de ahorro/corriente, asignación de número único, asociación a cliente |
| **Depósitos** | Registro de ingreso de dinero, actualización de saldo, generación de comprobante |
| **Retiros** | Registro de salida de dinero, validación de saldo suficiente, generación de comprobante |
| **Transferencias** | Movimiento de dinero entre cuentas, validación de saldo y cuenta destino |
| **Consulta de saldo** | Visualización del saldo actual de una o varias cuentas |
| **Historial de transacciones** | Listado de movimientos con filtros por fecha y tipo |
| **Pagos de servicios** | Pago de facturas (luz, agua, etc.), validación de monto y proveedor |
| **Administración de usuarios** | CRUD de usuarios del sistema, asignación de roles y permisos |

---

##  Estructura del proyecto

```
banco-sistema/
│
├── .github/
│   └── workflows/          # CI/CD (tests, linters, deploy)
│
├── src/
│   ├── auth/
│   ├── clientes/
│   ├── cuentas/
│   ├── transacciones/
│   │   ├── depositos/
│   │   ├── retiros/
│   │   ├── transferencias/
│   │   └── historial/
│   ├── consultas/
│   │   └── saldo/
│   ├── pagos/
│   └── administracion/
│
├── tests/
├── docs/
├── config/
├── .env.example
├── .gitignore
├── README.md
└── CONTRIBUTING.md
```

---

##  Reparto del trabajo entre aprendices

El desarrollo se dividió en partes iguales entre los dos aprendices, asignando 5 módulos (features) a cada uno. Cada aprendiz fue responsable de crear su rama, desarrollar la funcionalidad, hacer sus propios commits y abrir el Pull Request correspondiente hacia `develop`.

### Jhojan Franco

| Rama | Módulo |
|---|---|
| `feature/login` | Login |
| `feature/registro-clientes` | Registro de clientes |
| `feature/apertura-cuentas` | Apertura de cuentas |
| `feature/depositos` | Depósitos |
| `feature/retiros` | Retiros |

### Jhostin Balza

| Rama | Módulo |
|---|---|
| `feature/transferencias` | Transferencias |
| `feature/consulta-saldo` | Consulta de saldo |
| `feature/historial-transacciones` | Historial de transacciones |
| `feature/pagos-servicios` | Pagos de servicios |
| `feature/administracion-usuarios` | Administración de usuarios |

---

##  Historial de ramas y commits (evidencia de participación)

Para comprobar el aporte individual de cada aprendiz, se puede consultar el historial de commits por rama y por autor con los siguientes comandos:

### Ver todas las ramas del repositorio (locales y remotas)
```bash
git branch -a
```

### Ver el historial de commits de una rama específica
```bash
git log feature/login --oneline
git log feature/transferencias --oneline
```

### Ver los commits agrupados por autor (para todo el repositorio)
```bash
git log --pretty=format:"%h - %an, %ad : %s" --date=short
```

### Ver solo los commits de un aprendiz específico
```bash
git log --author="Jhojan Franco" --oneline
git log --author="Jhostin Balza" --oneline
```

### Ver un resumen de commits por autor (cantidad de aportes)
```bash
git shortlog -sn --all
```

**Ejemplo de salida esperada:**
```
15  Jhojan Franco
14  Jhostin Balza
```

### Ver el historial gráfico de ramas fusionadas a develop
```bash
git log --graph --oneline --all
```

Este comando permite visualizar en consola cómo cada rama `feature/*` fue creada desde `develop` y luego fusionada nuevamente, dejando evidencia clara de qué aprendiz trabajó en cada módulo y en qué momento.

>  **Nota:** para que este historial refleje correctamente la autoría de cada aprendiz, cada uno debe hacer sus commits desde su propia cuenta de GitHub (o configurar `git config user.name` y `git config user.email` correctamente en su entorno local antes de hacer commit).

---

##  Seguridad

Al ser un sistema bancario, se recomienda:
- Mantener el repositorio **privado**.
- No subir credenciales, tokens ni claves (usar `.env` y agregarlo a `.gitignore`).
- Aplicar revisión de código obligatoria antes de cada merge.
- Ejecutar análisis de seguridad (SAST) en el pipeline de CI.
