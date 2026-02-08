# Requisitos no funcionales

**RNF-1: Rendimiento**\
La aplicación debe cargar las pantallas principales en menos de 2 segundos y la búsqueda de jugadores o equipos debe mostrar resultados en menos de 1 segundo. Las actualizaciones de clasificaciones y estadísticas deben reflejarse casi en tiempo real, incluso con varias ligas activas.

**RNF-2: Seguridad**\
Todos los datos sensibles, como contraseñas o información personal, deben almacenarse de manera segura (hash y cifrado). El sistema debe controlar el acceso a funcionalidades según los roles asignados y protegerse frente a ataques comunes como XSS o SQL Injection. Los administradores podrán utilizar autenticación multifactor para mayor seguridad.

**RNF-3: Usabilidad**\
La app debe ser intuitiva y fácil de usar, con interfaces claras y consistentes. La navegación entre pantallas debe ser sencilla y permitir completar tareas como crear ligas, registrar resultados o consultar estadísticas sin dificultades.

**RNF-4: Disponibilidad**\
El sistema debe garantizar un tiempo de actividad mínimo del 99%. El backend debe poder recuperarse de fallos sin pérdida de datos importantes y permitir restablecer ligas o estadísticas si se reinicia la temporada con los mismos equipos.

**RNF-5: Compatibilidad**\
La aplicación debe funcionar correctamente en dispositivos Android e iOS, incluyendo versiones recientes y al menos 2-3 versiones anteriores. La versión web debe mantener las mismas funcionalidades y estilo visual.

**RNF-6: Escalabilidad**\
El sistema debe soportar un aumento de usuarios, ligas y partidos sin afectar significativamente el rendimiento. Debe permitir añadir nuevas funcionalidades como estadísticas avanzadas o nuevos roles sin reescribir gran parte del código.

**RNF-7: Mantenimiento**\
El código debe estar limpio y bien documentado para facilitar futuras modificaciones. Debe existir un sistema de logs que permita identificar errores o incidencias críticas y separar claramente frontend y backend para actualizar componentes de forma independiente.

**RNF-8: Internacionalización**\
La aplicación debe adaptarse a distintos idiomas y formatos regionales (fecha, hora) permitiendo la futura inclusión de más idiomas sin reestructurar la interfaz.

**RNF-9: Copias de seguridad**\
Se deben realizar backups automáticos de la base de datos y la información crítica. La app debe permitir restaurar datos en caso de fallo, asegurando continuidad del servicio y preservación de estadísticas y resultados históricos.
