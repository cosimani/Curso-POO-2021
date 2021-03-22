.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 03 - POO 2021
===================
(Fecha: 23 de marzo)


Función Genérica
================

- Supongamos que debemos implementar una función que imprima en la salida los valores de un array de enteros:

.. code-block:: c

	void imprimir ( int v[], int cantidad )  {
	    for ( int i = 0 ; i < cantidad ; i++ )
	        cout << v[ i ] << " ";
	}

	int main()  {
	    int v1[ 5 ] = { 5, 2, 4, 1, 6 };
	    imprimir( v1, 3 );
	}

- Ahora necesitamos la impresión de un array de float

.. code-block:: c

	void imprimir( float v[], int cantidad );

- Vemos que las versiones se diferencian por el tipo de datos del array. Entonces podemos utilizar lo siguiente:

.. code-block:: c

	template <class T> void imprimir ( T v[], int cantidad )  {
	    for ( int i=0 ; i < cantidad ; i++ )
	        cout << v[ i ] << " ";
	}

	int main()  {
	    int v1[ 5 ] = { 5, 2, 4, 1, 6 };
	    float v2[ 4 ] = { 2.3, 5.1, 0, 2 };

	    imprimir( v1, 5 );  // qué pasa pongo cantidad 10 -> Publica basura 
	    imprimir( v2, 2 );
	}

- El compilador utiliza el código de la función genérica como plantilla para crear automáticamente dos funciones sustituyendo T por el tipo de dato concreto.

.. code-block:: c

	Con T = int     utiliza -->     void imprimir( int v[], int cantidad )

	Con T = float   utiliza -->     void imprimir( float v[], int cantidad )

- Aquí, la única operación que realizamos sobre los valores de tipo T es:

.. code-block:: c

	cout << v[ i ]

- Esto pone una restricción, ya que sólo se admitirá los tipos de datos para los que se puedan imprimir en pantalla con:

.. code-block:: c

	cout <<

**Ejercicio 4**

- Escribir en C++ una función genérica para ordenar e imprimir un array (sólo tipos int, float y char). Que la publicación sea ordenada utilizando el método de ordenamiento por inserción.



Utilidades de la biblioteca estándar de C++
===========================================

vector
^^^^^^

- Mantiene sus elementos en un área contigua de memoria.
- El acceso aleatorio es eficiente.
- La inserción en cualquier posición distinta a la última es ineficiente.
- Se encuentra en #include <vector> en el namespace std

.. code-block:: c

	vector< int > v1;                     // vector vacío
	vector< int > v2( 15 );               // vector de 15 elementos
	vector< string > v3( 18, "cadena" );  // 18 elemento con valor inicial
	vector< string > v4( v3 );            // v4 es una copia v3

**Algunas operaciones**

.. code-block:: c

	size()          // Tamaño
	bool empty()    // Está vacío?
	void clear()    // Limpia el vector
	front()         // Acceso al primero
	back()          // Al último
	push_back( x )  // Inserción al último
	pop_back()      // Elimina
	w = v           // Asignación
	v == w   v < w  // Comparaciones
	v.at( i )       // Acceso con verificación de rango (lanza out_of_range)
	v[ i ]          // Acceso sin verificación de rango



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



**Ejercicio:** Escribir la salida por consola de la siguiente aplicación:

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

