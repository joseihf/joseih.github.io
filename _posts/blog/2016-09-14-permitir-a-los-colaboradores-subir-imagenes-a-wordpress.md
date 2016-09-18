---
layout: post
title: "Permitir a los colaboradores subir imágenes a Wordpress"
modified:
author: ji
categories: blog
excerpt:
tags: [Wordpress]
share: true
image:
    feature: wordpress.jpg
    thumb: wordpress-thumb.jpg
    credit: Pixabay
    creditlink: https://pixabay.com/es/
date: 2016-09-14
#modified: 2016-08-28
comments: true
---

Cuando usas un Wordpress con distintos usuarios y quieres permitir a estos para que puedan crear entradas en el blog te puedes encontrar con un problema. El rol "colaborador", quizás el que mejor se ajusta a esta situación, no permite que estos puedan subir las imágenes. Para solucionar esto, tan solo tendremos que añadir algo de código a nuestro Wordpress.

Lo primero que hay que hacer es editar el archivo functions.php de tu tema de apariencia. Para ello, lo más sencillo es acceder a "Apariencia - editor" de la parte de administración de nuestro Wordpress y seleccionar "functions.php". A continuación, añade el siguiente código:

```php
if ( current_user_can('contributor') && !current_user_can('upload_files') )
     add_action('admin_init', 'allow_contributor_uploads');
     
     function allow_contributor_uploads() {
          $contributor = get_role('contributor');
          $contributor->add_cap('upload_files');
     }
```

Y eso es todo. A partir de ahora tus usuarios con el rol **Colaboradores** podrán subir las imágenes sin problema.