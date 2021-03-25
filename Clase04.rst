.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 04 - POO 2021
===================
(Fecha: 25 de marzo)



Cadena de caracteres
^^^^^^^^^^^^^^^^^^^^

- Al estilo C	

.. code-block:: c

	#include <string.h>

	char cadena1[ 30 ], cadena2[ 30 ];
	strcpy( cadena1, "Hola" );
	cin >> cadena2;
	
- Con C++ usamos   

.. code-block:: c

	#include<string>

	Asignación       s1 = s2    s1 = "Hola"
	Concatenación    s1 = s2 + s3	
	Comparación      if ( s1 == s2 )
	Subcadenas       s1.substr( 3, 5 )
	Longitud         s1.length()    s2.size()  // Son lo mismo
	Acceso a char    s1[ 2 ]    s2.at( 2 )  // Lanza out_of_range
	Limpiar          s1.clear()
	Busca cadena     s1.find( "cadena" );    s1.find( s2 );
	Puntero a char   const char *c = s1.c_str()




Punteros
========

**Declaración**

.. code-block:: c

	int * entero;     // entero es un puntero a int
	char * caracter;  // puntero a char

	entero      es el puntero
	*entero     es el contenido


**Punteros a variables**

.. code-block:: c

	int entero;         // entero es una variable int
	int * pEntero;      // pEntero es un puntero a int
	pEntero = &entero;  // &entero es la dirección de memoria donde se almacena entero

**Arrays y punteros**

.. code-block:: c

	int miArray[ 10 ];	// miArray es como un puntero al primer elemento
	int* puntero;

	puntero = miArray;  // similar a:  puntero = &miArray[0];
	( *puntero )++;       // equivale a miArray[0]++;  // incrementa
	puntero++;          // equivale a &miArray[1];  // se mueve una posición

	puntero = puntero + 3;  // se desplaza 3 posiciones int



**Ejercicio 5:** Escribir la salida por consola de la siguiente aplicación:

.. code-block:: c

	#include <QApplication>
	#include <QDebug>

	int main( int argc, char** argv )  {
	    QApplication app( argc, argv );

	    int a = 10, b = 100, c = 30, d = 1, e = 54;
	    int m[ 10 ] = { 10, 9, 80, 7, 60, 5, 40, 3, 20, 1 };
	    int *p = &m[ 3 ], *q = &m[ 6 ];

	    ++q;
	    qDebug() << a + m[ d / c ] + b-- / *q + 10 + e--;

	    p = m;
	    qDebug() << e + *p + m[ 9 ]++;

	    return 0;
	}


**Ejercicio 6**

- Crear un vector de 100 números enteros.
- Los valores serán aleatorios y positivos menores o iguales a 10.
- Utilizar un algoritmo para ordenar de menor a mayor estos números.


**Ejercicio 7**

- Crear dos std::vector. Un vector< double > y un vector< double * >
- Agregar 10 elementos en cada uno.
- Averiguar cuál objeto ocupa más memoria. 
- Publicar por consola el tamaño.


**Entregar estos ejercicios**

- Luego de finalizar el desarrollo del programa, cerrar el proyecto de QtCreator.
- Eliminar el archivo .pro.user
- Comprimir cada ejercicio por separado (por ejemplo: ejercicio6.zip y ejercicio7.zip).
- Enviar un mail a cesarosimani@gmail.com (Asunto: POO 2021 - Ejercicio 6 y 7).




