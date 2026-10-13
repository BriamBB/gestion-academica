# Sistema de Matrícula Académica Universitaria · Base de Datos Relacional

Proyecto de la asignatura de Bases de Datos, Facultad de Ingeniería, Fundación Universitaria Compensar.

**Integrantes:** Ángel Ricardo Joya Patiño, Michael Stiven León Jiménez, Juan Sebastián Castro Dávila y Brian Steivin Blanco Chamorro.

**Motor de base de datos:** MariaDB 10.4 sobre XAMPP.

## Descripción

La matrícula académica necesita información confiable para inscribir materias, controlar cupos y revisar prerrequisitos. Este proyecto convierte el modelo entidad-relación diseñado en el momento 1 en una base de datos funcional llamada `gestion_academica`, y comprueba su funcionamiento con scripts SQL.

La base resuelve tres problemas:

- **Prerrequisitos:** evita inscribir a un estudiante en un curso sin haber aprobado los requeridos.
- **Cupos:** impide que un grupo supere su capacidad.
- **Horarios:** permite identificar posibles cruces entre los grupos elegidos.

## Modelo de datos

La base tiene 7 tablas. Las relaciones de muchos a muchos se resuelven con tablas intermedias.

| Tabla | Descripción |
| --- | --- |
| `facultad` | Facultades de la universidad y sus decanos. |
| `estudiante` | Datos personales y programa académico. |
| `curso` | Materias con sus créditos y la facultad a la que pertenecen. |
| `prerrequisito` | Cursos que se deben aprobar antes de ver otro curso. |
| `grupo` | Grupos de cada curso, con horario, profesor y cupos. |
| `matricula` | Inscripción de un estudiante en un grupo. |
| `registro_academico` | Historial del estudiante: cursos, notas y periodo. |

### Reglas de integridad

- Llaves primarias autoincrementales y llaves foráneas entre las tablas.
- Valores únicos: nombre de facultad, correo del estudiante y nombre del curso.
- Rangos válidos: semestre de 1 a 12, créditos de 1 a 10 y nota final de 0 a 5.
- El cupo disponible nunca supera el cupo máximo.
- Estados limitados: la matrícula solo puede estar Activa, Retirada o Cancelada, y el registro académico Cursando, Aprobado, Reprobado o Retirado.

## Contenido del repositorio

```
├── docs/                      # Documento del proyecto (formato IEEE) y presentación
├── sql/
│   └── mariadb/
│       ├── gestion_academica.sql         # Crea la base de datos, las tablas y las relaciones
│       ├── gestion_academica_insert.sql  # Datos ficticios de prueba
│       └── consultas/
│           ├── 01_DDL.sql   # Modificación de estructura (ALTER)
│           ├── 02_DML.sql   # INSERT / UPDATE / DELETE
│           ├── 03_DQL.sql   # Consultas SELECT, JOIN, GROUP BY
│           ├── 04_VDL.sql   # Vistas
│           ├── 05_DCL.sql   # Usuarios y permisos
│           └── 06_TCL.sql   # Transacciones
└── README.md
```

> Los archivos `glob_gusters*.sql`, `check-mariadb.sql`, la carpeta `tests` y los PDF de ejemplo en `docs` corresponden al ejemplo del videoclub entregado en clase, que sirvió como guía de estructura.

## Cómo ejecutarlo

1. Abre el **Panel de Control de XAMPP** y arranca **Apache** y **MySQL**.
2. Abre una terminal en la carpeta del proyecto y conéctate a MariaDB:

```
C:\xampp\mysql\bin\mysql.exe -u root
```

3. Ejecuta los scripts en este orden, con el comando `source`:

```
source sql/mariadb/gestion_academica.sql
source sql/mariadb/gestion_academica_insert.sql
source sql/mariadb/consultas/01_DDL.sql
source sql/mariadb/consultas/02_DML.sql
source sql/mariadb/consultas/03_DQL.sql
source sql/mariadb/consultas/04_VDL.sql
source sql/mariadb/consultas/05_DCL.sql
source sql/mariadb/consultas/06_TCL.sql
```

4. Verifica el resultado en **phpMyAdmin** (`http://localhost/phpmyadmin`): selecciona la base `gestion_academica`. Las relaciones se ven en **More** (Más), luego **Designer** (Diseñador).

Los scripts de creación e inserción se pueden ejecutar varias veces sin errores.

## Entregables

- **Documento:** formato IEEE, en la carpeta `docs`.
- **Presentación:** en la carpeta `docs`.
- **Video de la ejecución:** [Ver video](PEGA_AQUI_EL_ENLACE_DEL_VIDEO)

## Créditos y licencia

La estructura del repositorio se basa en el ejemplo Glob-Gusters Video-Club entregado en clase. El proyecto se distribuye bajoNSE](LICENSE).
