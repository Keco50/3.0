# 3.0
Sistema Operativo 3
# Practica 1: Gestion de Paquetes y Repositorios en RHEL

# Actualizar los repositorios del sistema
dnf update -y && dnf upgrade -y

# 2. Listar los repositorios actualmente en uso
dnf repolist all

# 3. Buscar la herramienta en los repositorios
dnf list bashtop

# 4. Instalar Bashtop si está disponible
dnf install -y bashtop

# 5. Si no está disponible, agregarlo al repositorio local
dnf install -y epel-release
dnf install -y bashtop

# 6. Verificar que la herramienta está instalada
bashtop

# 7. Desinstalar Bashtop junto con sus archivos de configuración
dnf remove -y bashtop

# 8. Eliminar todas las dependencias que ya no estén en uso
dnf autoremove -y

# Practica 2: Automatización con Cron y At

# 1. Crear un trabajo en cron para actualizar el sistema a las 11 p.m. todos los días
echo "0 23 * * * root dnf update -y && dnf upgrade -y" | tee -a /etc/crontab

# 2. Programar el reinicio del sistema todos los domingos a las 3 a.m.
echo "0 3 * * 0 root /sbin/shutdown -r now" | tee -a /etc/crontab

# 3. Crear una tarea con 'at' para eliminar el contenido de /tmp en 1 minuto
echo "rm -rf /tmp/*" | at now + 1 minute

# 4. Verificar la tarea en cola
atq

# 5. Mostrar el resultado después de la ejecución
ls -la /tmp
