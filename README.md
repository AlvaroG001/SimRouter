# SimRouter

SimRouter es un proyecto diseñado para gestionar automáticamente servidores virtuales y redes utilizando herramientas como QEMU, libvirt y Open vSwitch. Este proyecto permite crear, configurar, monitorizar y realizar operaciones con máquinas virtuales según especificaciones predefinidas.

---

## Tabla de Contenidos

1. [Descripción del Proyecto](#descripción-del-proyecto)
2. [Estructura del Proyecto](#estructura-del-proyecto)
3. [Requisitos](#requisitos)
4. [Configuración](#configuración)
5. [Uso](#uso)
6. [Ejemplos de Salida](#ejemplos-de-salida)
7. [Contribución](#contribución)
8. [Licencia](#licencia)

---

## Descripción del Proyecto

El objetivo principal de SimRouter es automatizar la gestión de máquinas virtuales (VMs) y redes virtuales, permitiendo la creación de entornos simulados de manera eficiente. Entre las funcionalidades principales, el proyecto ofrece:

- Creación automática de máquinas virtuales a partir de una imagen base utilizando `qemu-img` y `libvirt`.
- Configuración de redes virtuales mediante `Open vSwitch`.
- Configuración personalizada de servicios en las VMs, como servidores web Apache y balanceadores de carga HAProxy.
- Gestión del ciclo de vida de las VMs (inicio, apagado, destrucción y conexión a consolas).
- Eliminación automatizada de recursos creados (VMs, redes, archivos de configuración).
- Configuración detallada y adaptada según los parámetros especificados en un archivo de configuración JSON.

---

## Estructura del Proyecto

La estructura básica del proyecto es la siguiente:

```
SimRouter/
├── manage-p2.json         # Archivo de configuración JSON.
├── manage-p2.py           # Archivo principal del proyecto.
├── lib_vm.py              # Módulo auxiliar para la gestión de máquinas virtuales.
└── README.md              # Documentación del proyecto.
```

### Imagen de la estructura

Aquí puedes incluir una imagen representativa de la estructura del proyecto:

**[Inserta la imagen aquí]**

---

## Requisitos

Para ejecutar SimRouter, asegúrate de tener instalado lo siguiente:

- Python 3.8 o superior.
- Las siguientes dependencias de Python (incluidas en la biblioteca estándar):
  - `json`
  - `logging`
  - `os`
  - `subprocess`
  - `sys`
- Herramientas adicionales:
  - `qemu-img`
  - `virsh` (parte de libvirt)
  - `ovs-vsctl` (parte de Open vSwitch)

---

## Configuración

El archivo `manage-p2.json` es la base de la configuración del proyecto. Este archivo debe tener el siguiente formato:

```json
{
    "number_of_servers": 3,
    "debug": true
}
```

### Parámetros:

- `number_of_servers`: Número total de servidores que serán gestionados por el proyecto.
- `debug`: Si es `true`, se activará el modo detallado de logging (DEBUG); si es `false`, se mostrará solo información básica (INFO).

---

## Uso

Sigue los pasos a continuación para ejecutar SimRouter:

1. Asegúrate de haber configurado correctamente el archivo `manage-p2.json`.
2. Ejecuta el archivo principal del proyecto:

   ```bash
   python manage-p2.py
   ```

3. Los logs se mostrarán en la consola y, si está configurado, también se guardarán en archivos de logs.

### Funcionalidades Principales:

1. **Creación de Máquinas Virtuales (VMs):**
   - Las VMs se crean utilizando una imagen base QCOW2 y configuraciones específicas definidas en el código.
   - Cada VM tiene su propio archivo XML para la definición en libvirt.

2. **Configuración de Redes Virtuales:**
   - Se utilizan bridges creados con `Open vSwitch` para interconectar las VMs.

3. **Gestión de Servicios en las VMs:**
   - Los servidores web Apache y el balanceador de carga HAProxy se configuran automáticamente según el rol de cada VM.

4. **Eliminación de Recursos:**
   - Al finalizar, el proyecto elimina las VMs, redes virtuales y archivos de configuración generados.

---

## Ejemplos de Salida

### Configuración con `debug: true`

```bash
2024-12-10 12:00:00 - DEBUG - Creando red virtual: lan1
2024-12-10 12:00:01 - DEBUG - Red lan1 creada correctamente.
2024-12-10 12:00:02 - DEBUG - Creando máquina virtual: s1
2024-12-10 12:00:03 - DEBUG - Máquina virtual s1 creada correctamente.
2024-12-10 12:00:04 - DEBUG - Configurando HAProxy en lb.
2024-12-10 12:00:05 - DEBUG - Configuración completada.
```

### Configuración con `debug: false`

```bash
2024-12-10 12:00:00 - INFO - Inicializando entorno virtual...
2024-12-10 12:00:05 - INFO - Entorno configurado correctamente.
```

---

## Contribución

Si deseas contribuir a este proyecto, sigue los pasos a continuación:

1. Haz un fork del repositorio.
2. Crea una rama para tu funcionalidad o corrección:

   ```bash
   git checkout -b nombre-de-tu-rama
   ```

3. Realiza los cambios y haz un commit:

   ```bash
   git commit -m "Descripción de los cambios"
   ```

4. Sube tus cambios a tu rama remota:

   ```bash
   git push origin nombre-de-tu-rama
   ```

5. Abre un Pull Request en el repositorio principal.

---

## Licencia

Este proyecto está licenciado bajo la [Licencia MIT](https://opensource.org/licenses/MIT). Puedes usarlo libremente, modificarlo y distribuirlo bajo los términos de esta licencia.
