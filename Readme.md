# EDUCATATIONAL PURPOSES ONLY

Este contenido es educacional e inspirado en su autor: Idea Visuals Tech, es un extra, un programa que he diseñado para hacerlo mas facil.

[![Video de Introducción](https://youtu.be/YOdxlBLbekc?si=78g5_6U5H1hhrHQN)

Mis gracias a Idea Visuals Tech

Para un enfoque más eficiente, podemos usar un script basado en el calendario, ejecutado el día exacto en que quieras (por ejemplo, cada 85 días) en lugar de mantener un **LaunchDaemon** en segundo plano todo el tiempo. Esto se puede lograr con el programador de tareas de macOS, **`cron`**.

## Configuración basada en el calendario

### Paso 1: Crear el script
1. Abre **Terminal** y crea un script como antes:
   ```bash
   nano ~/clean_final_cut.sh.sh
   ```
2. Añade el contenido al script:
   ```bash
   #!/bin/bash

   # Eliminar archivos de Final Cut
   rm -rf ~/Library/Application\ Support/ProApps/Trial.plist
   ```

3. Guarda y cierra el archivo (`Ctrl+O`, `Enter`, `Ctrl+X`).

4. Haz que el script sea ejecutable:
   ```bash
   chmod +x ~/clean_final_cut.sh.sh
   ```

---

### Paso 2: Configurar una tarea cron

1. Abre el archivo de configuración de cron:
   ```bash
   crontab -e
   ```

2. Añade esta línea al final del archivo para programar la ejecución del script cada 85 días (por ejemplo, el día 1 de un conjunto de meses):
   ```bash
   0 0 1 */3 * /bin/bash ~/clean_final_cut.sh.sh
   ```

   **Explicación del cron:**
   - `0 0 1 */3 *` -> Ejecuta a las 00:00 horas del día 1 cada 3 meses.
   - `~/clean_final_cut.sh.sh` -> Ruta del script.

3. Guarda y cierra (`Ctrl+O`, `Enter`, `Ctrl+X`).

---

### Paso 3: Verificar la configuración de cron
Para verificar que tu tarea cron se haya guardado correctamente, usa:
```bash
crontab -l
```

Esto mostrará las tareas programadas en tu sistema. Deberías ver la línea que acabas de agregar.

#### ¿Por qué este método es mejor?
1. **Eficiencia:** Solo se ejecuta el día programado. El sistema no utiliza recursos adicionales innecesarios.
2. **Predecible:** La tarea está basada en el calendario y ocurre de manera precisa.
3. **Sin Daemons persistentes:** No hay necesidad de mantener un proceso en ejecución.
