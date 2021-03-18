.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 01 - POO 2021
===================
(Fecha: 16 de marzo)

    :Autor: César Osimani
    :Mail: cesarosimani@gmail.com
    :Fecha: 16 de marzo de 2021
    :Regularidad: 
	    - 2 parciales 
	    - Parcialitos, ejercicios y cuestionarios (3er nota)
	    - Los ejercicios son algunos de los que están en las clases
	    - Los ejercicios, si están como pide el enunciado se tiene un 8, para llegar al 10 tiene que ser sobresaliente, con agregados extras originales.
    :Proyecto integrador final: 
	    - Un trabajo integrador individual se puede presentar para el final (tema a elección)
    :Proyecto integrador parcial: 	   
	    - Trabajo individual se puede presentar en lugar de los dos parciales tradicionales
	    - Se van entregando avances del trabajo en las fechas de los parciales
	    - Si las entregas de avances del trabajo están para promocionar la materia, igualmente el trabajo tiene que estar finalizado durante el cursado. De lo contrario se entrega en la fecha del examen final rindiendo normalmente.
	    - En época de pandemia se decidió, desde la universidad, que no hay promoción de asignaturas.
    :Trabajos propuestos: 
        - **Spotify y control de luces de ambiente**: Hay un trabajo ya iniciado y funcionando de un alumno que utiliza la API de Spotify para reproducir canciones y controlar las luces Philips Hue. La propuesta sería modificar el proyecto para controlar cualquier tipo de luces a través de alguna interfaz electrónica (Arduino o Raspberry) y que la intensidad de la iluminación esté definida por la intensidad o dinámica de la canción. Como alternativa se puede controlar una tira de leds RGB.
        - **Mapa de calor de las fotos publicadas**: Trabajo iniciado por alumnos que utilizan la API de Facebook o Instagram para extraer información de la ubicación de cada foto para hacer un mapa de calor sobre un mapa de Google con la cantidad de fotos. La propuesta es redefinir la interfaz gráfica de usuario.
        - **Opcionables**: Continuar el desarrollo de la aplicación Opcionables para redefinir la GUI.
        - **Redes neuronales**: Utilizando Python con la biblioteca PyQt utilizando POO.
        - **Procesamiento de imágenes**: Utilizando Python con la biblioteca PyQt utilizando POO.
        - **Buscar en mercadolibre con imágenes**: Utilizar la API de mercadolibre y de Cloud Vision de Google para colocar una imagen y busque ofertas. Ver https://cloud.google.com/vision/docs/drag-and-drop
        - **Combinar APIs**: Youtube Music, Instagram, TIkTok, Google, etc.

    :Temas principales: 
		- Espacio de nombres
		- inline y const
		- std, vector, string
		- Aritmética de punteros
		- Funciones genéricas
		- Herencia y herencia múltiple
		- Polimorfismo
		- Funciones virtuales
		- Clases abstractas
		- Modificador friend
		- Biblioteca Qt
			- Uso de documentación
			- slots y signals
			- QtNetwork
			- Interfaz gráfica de usuario (widgets, layouts, etc.)
			- QPainter y captura de eventos del teclado y del mouse
			- QTimer
			- QtDesigner
		- OpenGL (glOrtho, gluPerspective, glLookAt, rotación, traslación, texturas, ...)
		- Base de datos (SELECT e INSERT).
		- Resolver los problemas consultando documentación técnica de distintas fuentes


Biblioteca estándar de C++
==========================

- Está en el espacio de nombres ``std``
- En la biblioteca estándar de C, los archivos de cabecera X.h se reemplazan por cX o X. Por ejemplo:

.. code-block:: c

	#include <stdlib.h>                   #include <cstdlib>    

	    int atoi( const char * )  // Convierte a int un número expresado en cadena
	    int abs( int )            // Devuleve el valor absoluto
	    int rand()                // Devuelve un pseudo número aleatorio entre 0 y 32767


	#include <stdio.h>                   #include <cstdio>    

	    // Borra un archivo. DEvuelve 0 o un código de error.
	    int remove( const char * filename )

	    // imprime por pantalla. Recibe un número indefinido de argumentos.
	    int printf( const char * format, ... )

	#include <iostream.h>                   #include <iostream>    

	    cout
	    cin
	    endl


**Ejercicio 1**

- Instalar Qt Creator, junto con la biblioteca Qt y las herramientas de compilación MinGW.
- Utilizar el instalador Offline: https://download.qt.io/archive/qt/5.14/5.14.1/

