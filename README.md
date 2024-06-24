# Mesop Manual

## Introducción

Este manual proporciona instrucciones detalladas y ejemplos de uso para el comando `mesop`. Este comando se ejecuta en el entorno Termux en Android y utiliza diversas banderas (flags) para ajustar su comportamiento.

## Uso Básico

El comando `mesop` se utiliza de la siguiente manera:

```
/data/data/com.termux/files/usr/bin/mesop [flags]
```

Las banderas (flags) permiten personalizar la ejecución del comando. A continuación se detallan las diferentes categorías de banderas y su uso.

## Banderas Disponibles

### absl.app

#### Mostrar Ayuda

- `-?`, `--[no]help`
  - Muestra esta ayuda.
  - Default: `false`.

- `--[no]helpfull`
  - Muestra ayuda completa.
  - Default: `false`.

- `--[no]helpshort`
  - Muestra ayuda corta.
  - Default: `false`.

- `--[no]helpxml`
  - Similar a `--helpfull`, pero genera salida en formato XML.
  - Default: `false`.

#### Validación de Argumentos

- `--[no]only_check_args`
  - Establece a true para validar los argumentos y salir.
  - Default: `false`.

#### Depuración y Perfilado

- `--[no]pdb`
  - Alias para `--pdb_post_mortem`.
  - Default: `false`.

- `--[no]pdb_post_mortem`
  - Establece a true para manejar excepciones no capturadas con PDB post mortem.
  - Default: `false`.

- `--profile_file`
  - Vuelca la información del perfil en un archivo (para `python -m pstats`). Implica `--run_with_profiling`.

- `--[no]run_with_pdb`
  - Establece a true para el modo de depuración con PDB.
  - Default: `false`.

- `--[no]run_with_profiling`
  - Establece a true para perfilar el script. La ejecución será más lenta y el formato de salida podría cambiar con el tiempo.
  - Default: `false`.

- `--[no]use_cprofile_for_profiling`
  - Usa cProfile en lugar del módulo profile para el perfilado. Esto no tiene efecto a menos que `--run_with_profiling` esté establecido.
  - Default: `true`.

### absl.logging

#### Registro de Logs

- `--[no]alsologtostderr`
  - ¿También registrar en stderr?
  - Default: `false`.

- `--log_dir`
  - Directorio para escribir archivos de registro.
  - Default: `''`.

- `--logger_levels`
  - Especifica el nivel de registro de los registradores. El formato es una lista CSV de `nombre:nivel`. Donde `nombre` es el nombre del registrador usado con `logging.getLogger()`, y `nivel` es un nombre de nivel (INFO, DEBUG, etc). Por ejemplo: `myapp.foo:INFO,other.logger:DEBUG`.
  - Default: `''`.

- `--[no]logtostderr`
  - ¿Debe registrar solo en stderr?
  - Default: `false`.

- `--[no]showprefixforinfo`
  - Si es False, no se antepone el prefijo a los mensajes de información cuando se registran en stderr, el nivel de --verbosity está en INFO, y se utiliza el registro de Python.
  - Default: `true`.

- `--stderrthreshold`
  - Registra mensajes en este nivel o más severos en stderr además del archivo de registro. Los valores posibles son 'debug', 'info', 'warning', 'error', y 'fatal'. Obsoleta `--alsologtostderr`. Usar `--alsologtostderr` cancela el efecto de esta bandera. Tenga en cuenta que esta bandera está sujeta a --verbosity y requiere que el archivo de registro no sea stderr.
  - Default: `fatal`.

- `-v`, `--verbosity`
  - Nivel de verbosidad del registro. Los mensajes registrados en este nivel o inferior se incluirán. Establezca en 1 para registro de depuración. Si la bandera no se estableció o suministró, el valor cambiará del valor predeterminado de -1 (advertencia) a 0 (información) después de analizar las banderas.
  - Default: `-1` (un entero).

### mesop.bin.bin

- `--[no]prod`
  - Establece a true para el modo de producción; de lo contrario, modo editor.
  - Default: `false`.

### mesop.runtime.context

- `--[no]enable_component_tree_diffs`
  - Establece a true para devolver diferencias en el árbol de componentes en las respuestas de eventos del usuario (en lugar del árbol completo).
  - Default: `true`.

### mesop.server.flags

- `--port`
  - Puerto para ejecutar el servidor Python.
  - Default: `32123` (un entero).

### absl.flags

- `--flagfile`
  - Inserta definiciones de banderas desde el archivo dado en la línea de comandos.
  - Default: `''`.

- `--undefok`
  - Lista separada por comas de nombres de banderas que está bien especificar en la línea de comandos incluso si el programa no define una bandera con ese nombre. IMPORTANTE: las banderas en esta lista que tienen argumentos DEBEN usar el formato --flag=value.
  - Default: `''`.

## Segunda Parte del Manual

Continuando con las banderas y su uso en el comando `mesop`.

### Ejemplos de Uso

Para entender mejor cómo utilizar estas banderas, a continuación se presentan algunos ejemplos prácticos.

### Ejemplo 1: Mostrar Ayuda

Para mostrar la ayuda completa de `mesop`, puedes utilizar la siguiente bandera:

```bash
/data/data/com.termux/files/usr/bin/mesop --helpfull
```

### Ejemplo 2: Ejecutar en Modo de Depuración

Para ejecutar `mesop` en modo de depuración con PDB, utiliza las siguientes banderas:

```bash
/data/data/com.termux/files/usr/bin/mesop --run_with_pdb
```

### Ejemplo 3: Ejecutar con Perfilado

Para ejecutar `mesop` con perfilado y guardar el perfil en un archivo, utiliza las siguientes banderas:

```bash
/data/data/com.termux/files/usr/bin/mesop --run_with_profiling --profile_file=perfil_info.txt
```

### Ejemplo 4: Configurar el Nivel de Registro

Para configurar el nivel de registro a `DEBUG` y también registrar en `stderr`, utiliza las siguientes banderas:

```bash
/data/data/com.termux/files/usr/bin/mesop --verbosity=1 --alsologtostderr
```

### Ejemplo 5: Ejecutar en Modo de Producción

Para ejecutar `mesop` en modo de producción, utiliza la siguiente bandera:

```bash
/data/data/com.termux/files/usr/bin/mesop --prod
```

### Ejemplo 6: Configurar Puerto del Servidor

Para configurar el puerto en el que se ejecuta el servidor Python, utiliza la siguiente bandera:

```bash
/data/data/com.termux/files/usr/bin/mesop --port=8080
```

### Ejemplo 7: Usar Archivo de Banderas

Para insertar definiciones de banderas desde un archivo, utiliza la siguiente bandera:

```bash
/data/data/com.termux/files/usr/bin/mesop --flagfile=flags.txt
```

### Ejemplo 8: Permitir Banderas Indefinidas

Para permitir banderas no definidas en la línea de comandos, utiliza la siguiente bandera:

```bash
/data/data/com.termux/files/usr/bin/mesop --undefok=flag1,flag2
```

## Resumen

El comando `mesop` es altamente configurable mediante el uso de varias banderas que permiten ajustar su comportamiento para diferentes necesidades. Este manual proporciona una guía para el uso básico y avanzado del comando. Para más detalles y ejemplos, se recomienda consultar la ayuda completa disponible mediante la bandera `--helpfull`.

## Contacto y Soporte

Para más información y soporte, puedes contactar al equipo de desarrollo o consultar la documentación oficial de `mesop`.

---

Este manual cubre la mayoría de las opciones y usos comunes de `mesop`. Para situaciones específicas y avanzadas, por favor consulta la documentación adicional o el soporte técnico adecuado.
