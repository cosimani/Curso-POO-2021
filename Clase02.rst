.. -*- coding: utf-8 -*-

.. _rcs_subversion:
  
Clase 02 - POO 2021
===================
(Fecha: 18 de marzo)


:Tarea para Clase 3:
	Ver `Tutorial Qt Creator - Introducción <https://www.youtube.com/watch?v=4TEED3VFBfc>`_ de `Videos tutoriales de Qt <https://www.youtube.com/playlist?list=PL54fdmMKYUJvn4dAvziRopztp47tBRNum>`_


Espacio de nombres (namespace)
==============================

- Permite agrupar declaraciones (de clases, funciones, etc.).
- Permite declarar identificadores (nombre de variables) sin que se solapen. Es decir, identificadores iguales en distinto namespace.
- Se pueden incluir las definiciones en un namespace pero mejor no.
- Un espacio de nombre es un ámbito.

Ejemplos con namespace
======================

**Ejemplo 1**

.. code-block:: c

	#include <iostream>
	using namespace std;

	namespace enteros  {
	    int var1 = 5;
	    int var2 = 7;
	}

	namespace con_decimales  {
	    float var1 = 5.14;
	    float var2 = 7.13;
	}

	int main()  {
	    cout << enteros::var1 << endl;
	    cout << con_decimales::var1 << endl;
	    return 0;
	}

- ¿Cuál es la salida por consola?

.. ..

 <!---  
 Publica:    5    5.14		(para ocultar requiere una primer linea con .. ..    Los que queremos ocultar debe tener el menos un espacio)
 --->

**Ejemplo 2**

.. code-block:: c

	#include <iostream>
	using namespace std;
	
	namespace enteros  {
	    int var1 = 5;
	    int var2 = 7;
	}
	
	namespace con_decimales  {
	    float var1 = 5.14;
	    float var2 = 7.13;
	}
	
	int main()  {
	    using enteros::var1;
	    using con_decimal::var2;

	    cout << var1 << endl;
	    cout << var2 << endl;
	    cout << enteros::var2 << endl;
	    cout << con_decimales::var1 << endl;

	    return 0;
	}

.. ..

 <!---  
 Publica:    5		7.13		7		5.14
 --->

**Ejemplo 3**

.. code-block:: c

	#include <iostream>
	using namespace std;

	namespace enteros  {
	    int var1 = 5;
	    int var2 = 7;
	}
	
	namespace con_decimales  {
	    float var1 = 5.14;
	    float var2 = 7.13;
	}

	int main()  {
	    using namespace enteros;

	    cout << var1 << endl;
	    cout << var2 << endl;
	    cout << con_decimales::var1 << endl;
	    cout << con_decimales::var2 << endl;

	    return 0;
	}

.. ..

 <!---  
 Publica:    5		7		5.14		7.13
 --->

**Ejemplo 4**

.. code-block:: c

	#include <iostream>
	using namespace std;

	namespace enteros  {
	    int var1 = 5;
	    int var2 = 7;
	}
	
	namespace con_decimales  {
	    float var1 = 5.14;
	    float var2 = 7.13;
	}
	
	int main()  {
	    {
	    using namespace enteros;
	    cout << var1 << endl;
	    }

	    {
	    using namespace con_decimales;
	    cout << var1 << endl;
	    }

	    return 0;
	}

.. ..

 <!---  
 Publica:    5		5.14
 --->


**Ejercicio 2**

- Crear el primer programa en Qt Creator un texto cualquier por consola utilizando el espacio de nombres std.


**Ejercicio 3**

- Compruebe el funcionamiento de los 4 ejemplos anteriores con espacio de nombres.
- Formule 2 preguntas sobre este tema para discutir en clase.


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

