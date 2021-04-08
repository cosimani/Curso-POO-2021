.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 06 - POO 2021
===================
(Fecha: 6 de abril)




.. ..
 
 <!---  
 **Función con número indefinido de parámetros** 

 (para ocultar requiere una primer linea con .. ..    Los que queremos ocultar debe tener el menos un espacio)

 - Requiere:

 .. code-block:: c

 	#include <cstdarg>

 - Imprime los enteros que se pasen como parámetro
 - Se puede comprender la sintaxis de:

 .. code-block:: c

 	int printf(const char* format, ...)

 .. code-block:: c

 	void imprimirParametros(int cantidad, ...)  {

 	    // En cstdarg se define un tipo va_list y define tres macros (va_start, va_arg y va_end)
 	    // para moverse por la lista de argumentos cuyo numero y tipo no son conocidos.
 
 	    // Aqui se declara la lista de parametros
 	    va_list argumentos; 
 				
 	    // La macro va_start inicializa 'argumentos' para ser usado por va_arg y va_end.
 	    // 'cantidad' es el nombre del ultimo parametro antes de la lista de argumentos.
 	    va_start(argumentos, cantidad); 
 
 	    for (int i=0 ; i<cantidad ; i++)  {
 
 		    // La macro va_arg contiene el tipo y el valor del proximo argumento. 
 			// Cada llamada a va_arg devuelve el resto de los argumentos.
 
 	        int valor = va_arg( argumentos, int );  // Devuelve en formato de int
 
 	        cout << valor << endl;
 	    }
 
 	    // A cada invocacion de va_start le corresponde una invocacion de va_end
 	    // en la misma funcion. 	   
 	    va_end(argumentos);  // Para limpiar la pila de parametros
 	}
 	
 **Ejercicio:** 
 
 - Definir una función (que se llame mi_printf) que realice el mismo trabajo que la famosa printf. 
 - Investigar qué tipos de datos se pueden utilizar en va_arg
 
 
 **Se puede pasar cualquier tipo siempre que sea con punteros:**
  
 .. code-block:: c
  
 	#include <QApplication>
 	#include <QString>
 	#include <QDebug>
 	#include <cstdarg>
 
 	void imprimirParametros(int cantidad, ...)  {
 	    va_list argumentos; // esta linea declara la lista de parametros
 	    va_start(argumentos, cantidad);
 
 	    for (int i=0 ; i<cantidad ; i++)  {
 	        QString *str = va_arg( argumentos, QString* );
 	        qDebug() << *str;
 	    } 
 
 	    va_end(argumentos);  // Para limpiar la pila de parametros
 	}
 
 	int main(int argc, char** argv)  {
 	    QApplication app(argc, argv);
 
 	    imprimirParametros(3, new QString("uno"), new QString("dos"), new QString("tres"),
 	                       new QString("cuatro"), new QString("cinco"));
 
 	    return 0;
 	}
 --->
 
 
**¿ Cómo funciona el método getDatos() ?**


.. code-block:: c

	class Poste  {
	private:
	    int altura;
	    int seccion;

	public:
	    Poste( int altura, int seccion );

	    void getDatos( int & altura, int & seccion );
	    void setDatos( int altura, int seccion );
	};

	Poste::Poste( int altura, int seccion ) : altura( altura ), seccion( seccion )  {
	    
	}

	void Poste::getDatos( int & altura, int & seccion )  {
	    altura = this->altura;
	    seccion = this->seccion;
	}

	void Poste::setDatos( int altura, int seccion )  {
	    this->altura = altura;
	    this->seccion = seccion;
	}



Convenciones para escribir nuestro código
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Los nombres de las clases, structs y enum comienzan con mayúsculas (usando ``UpperCamelCase``).
- Nombres de variables, funciones y métodos comienzan con minúsculas (usando ``lowerCamelCase`` y con palabras separadas con guión bajo).

- Ejemplos para nombres de clases: ``Persona`` - ``PrimeraClase`` - ``Ventana``
- Ejemplos para nombres de variables y funciones: ``velocidad`` - ``sumarNumeros`` - ``alto_imagen`` - ``anchoImagen``

**CamelCase**: Es escribir con la forma de jorobas de camello con las mayúsculas y minúsculas.

UpperCamelCase: La primera letra de cada palabra es mayúscula. Ejemplo: ``EjemploDeUpperCamelCase``.
lowerCamelCase: Igual a UpperCamelCase con excepción de la primer palabra. Ejemplo: ``ejemploDeLowerCamelCase``


**Ejercicio 8**

- Crear una clase Jugador con atributos ``int velocidad``, ``int fuerza`` y ``std::string nombre``
- Usar constructor inicializando de la manera recomendada la velocidad y fuerza en 0 y nombre "sin nombre" 
- Crear los métodos setter y getter para setear y obtener los valores de los atributos
- Incluir el destructor
- En la función main crear un ``std::vector< Jugador >`` e insertar 10 jugadores distintos
- Por último, publicar los datos de cada uno de los jugadores con ``std::cout``





Primer aplicación en Qt con interfaz gráfica
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Qt(Quasar Toolkit) 
	- Biblioteca para desarrollo de software de Quasar Technologies
	- Se llamó también Trolltech
	- Biblioteca multiplataforma
	- En el 2008 lo compró Nokia
	- Aplicaciones escritas con C++ (Qt)
		- KDE
		- VLC Media Player
		- Skype
		- VirtualBox
		- Google Earth 
		- Spotify para Linux
	- En 2012, Digia compra Qt y comercializa las licencias 
	- Digia desarrolló herramientas para usar Qt en iOS y Android.
		

**Ejemplo**

- Creación de una aplicación Qt

.. code-block:: c

	#include <QApplication>	
	// - Administra los controles de la interfaz
	// - Procesa los eventos
	// - Existe una única instancia
	// - Analiza los argumentos de la línea de comandos

	int main( int argc, char** argv )  {	
	    // app es la instancia y se le pasa los parámetros de la línea
	    // de comandos para que los procese.
	    QApplication app( argc, argv ); 

	    QLabel hola( "<H1 aling=right> Hola </H1>" );
	    hola.resize( 200, 100 );
	    hola.setVisible( true );

	    app.exec();  // Se le pasa el control a Qt
	    return 0;
	}
