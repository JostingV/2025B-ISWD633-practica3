# Aprendizaje 
Durante esta práctica, comprendi cómo persisten los datos en Docker, algo crucial para aplicaciones modernas. Pude dominar las tres estrategias de volúmenes y entender cuándo usar cada una.

## Lo que Aprendí sobre Cada Tipo de Volumen

**Bind Mounts:** Entendi que son para desarrollo porque sincronizan instantáneamente mis archivos locales con el contenedor (como sucedio con Nginx y WordPress). Esto me permite modificar código o HTML sin reconstruir imágenes. Sin embargo, entendí que no son ideales para producción por temas de seguridad y dependencia de la estructura del host.

**Volúmenes Nombrados:** Estos volumenes son el estándar profesional para producción, especialmente para bases de datos (PostgreSQL, MySQL) y datos críticos (Drupal). Lo bueno es que Docker los gestiona completamente, son portables y sobreviven aunque elimine o actualice contenedores. Esto garantiza que no pierda información importante.

**Volúmenes Anónimos:** Estos son temporales, útiles para cache o logs. Lo interesante fue aprender a limpiar usando `docker rm -v` y `docker volume prune` para evitar acumulación de volúmenes huérfanos que consumen espacio.


Al trabajar con WordPress/MySQL y Drupal/PostgreSQL, comprendí que debo crear redes personalizadas (`net-wp`, `net-drupal`) y usar nombres de contenedores como hostnames (ej: `server-postgres`) en lugar de IPs. 
