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
 
 
**¿ Cómo funciona el método ``getDatos`` ?**


.. code-block:: c

	class Poste  {
	private:
	    int altura;
	    int seccion;

	public:
	    Poste( int a, int s );

	    void getDatos( int & a, int & s );
	    void setDatos( int a, int s );
	};

	Poste::Poste( int a, int s )  {
	    altura = a;
	    seccion = s;
	}

	void Poste::getDatos( int & a, int & s )  {
	    a = altura;
	    s = seccion;
	}

	void Poste::setDatos( int a, int s )  {
	    altura = a;
	    seccion = s;
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

Signals y slots
^^^^^^^^^^^^^^^

- signal y slot son funciones.
- Las signals de una clase se comunican con los slots de otra.
- Se deben conectar con la función connect de QObject.
- Un evento puede generar una signal.
- Los slots reciben estas signals.
- SIGNAL() y SLOT() son macros (convierten a cadena).
- emisor y receptor son punteros a QObject


.. code-block:: c

	QObject::connect( emisor, SIGNAL( signal ), receptor, SLOT( slot ) );
	
- Se puede remover la conexión:

.. code-block:: c

	QObject::disconnect( emisor, SIGNAL( signal ), receptor, SLOT( slot ) );

**Ejemplo:** QPushButton para cerrar la aplicación.

.. code-block:: c

	#include <QApplication>
	#include <QPushButton>

	int main( int argc, char** argv )  {
	    QApplication a( argc, argv );
	    QPushButton* boton = new QPushButton( "Salir" );

	    QObject::connect( boton, SIGNAL( pressed() ), &a, SLOT( quit() ) );
	    boton->setVisible( true );
		
	    return a.exec();
	}

	

**Ejercicio 9:** 

- Crear una aplicación Qt que inicie con un botón que diga "Mostrar segundo boton y label"
- Al hacer clic sobre este botón se deberá ocultar este botón, se visualizará un nuevo botón y un label
- El segundo botón dirá "Ocultar label y mostrar boton final"
- Al hacer clic en el segundo botón, se ocultará este y el label, para mostrar el último botón
- El último botón dirá "Cerrar aplicacion" y cerrará la aplicación al presionarlo




QLineEdit
^^^^^^^^^

.. code-block:: c

	QLineEdit * le = new QLineEdit;
	le->setEchoMode( QLineEdit::Password );
	le->setEnabled( false );

	// QLineEdit::Normal  // Se visualizan al escribir
	// QLineEdit::NoEcho  // No se visualiza nada
	// QLineEdit::Password  // Se escribe como asteriscos
	// QLineEdit::PasswordEchoOnEdit  // Se escribe normal y al dejar de editar se convierten en asteriscos

**Señales**

.. code-block:: c

	// void returnPressed()  // Detecta cuando el usuario presiona Enter.

	// void editingFinished()  // Cuando pierde foco.

	// void textChanged( const QString & text )  // Texto modificado por código o por usuario desde la gui.

	// void textEdited( const QString & text )  // Sólo por el usuario.


QGridLayout
^^^^^^^^^^^

- Ubica los widgets en una grilla
- Con setColumnMinimumWidth() podemos setear el ancho mínimo de columna
- Separación entre widget con setVerticalSpacing( int )
- void addWidget( QWidget * widget, int fila, int columna, int spanFila, int spanCol )

Macro Q_OBJECT
^^^^^^^^^^^^^^

- Convierte a una clase cualquiera en una clase Qt.
- Una clase Qt permitirá trabajar con signals y slots.
- Incluir la macro Q_OBJECT en la primer línea de la definición de la clase.

	
**Ejemplo:** Control de volumen

.. code-block:: c

	#include <QApplication>
	#include <QWidget>
	#include <QHBoxLayout>
	#include <QSlider>
	#include <QSpinBox>

	int main( int argc, char** argv )  {
	    QApplication a( argc, argv );

	    QWidget * ventana = new QWidget;  // Es la ventana padre (principal)
	    ventana->setWindowTitle( "Volumen" ); 
	    ventana->resize( 300, 50 );

	    QSpinBox * spinBox = new QSpinBox;
	    QSlider * slider = new QSlider( Qt::Horizontal );
	    spinBox->setRange( 0, 100 );
	    slider->setRange( 0, 100 );

	    QObject::connect( spinBox, SIGNAL( valueChanged( int ) ), slider, SLOT( setValue( int ) ) );
	    QObject::connect( slider, SIGNAL( valueChanged( int ) ),  spinBox, SLOT( setValue( int ) ) );

	    spinBox->setValue( 15 );

	    QHBoxLayout * layout = new QHBoxLayout;
	    layout->addWidget( spinBox );
	    layout->addWidget( slider );
	    ventana->setLayout( layout );
	    ventana->setVisible( true );	

	    return a.exec();
	}

**Ejercicio 3**

- Cuando el valor del QSlider se modifique, colocar como título de la ventana el mismo valor (de 0 a 100). 
	

**Ejercicio**

- Explicación de este ejercicio en un `Video tutorial en Youtube ( https://youtu.be/T0tgFKFTl7c ) <https://youtu.be/T0tgFKFTl7c>`_
- Construir un login.
- Usar asteriscos para la clave.
- Detectar enter para simular la pulsación del botón.
- Si la clave ingresada es admin:admin, la aplicación se cerrará.
- Si se ingresa otra clave se borrará el texto de los QLineEdit.

- Tener en cuenta que este ejercicio requiere conocer cómo se define un slot propio.



.. ..
 
 <!---  

 **Resolución de este ejercicio**

 .. code-block:: c

	// main.cpp
	#include <QApplication>
	#include "login.h"

	int main(int argc, char** argv)  {
	    QApplication a(argc, argv);

	    Login login;
	    login.show();

	    return a.exec();
	}

	// login.h
	#include <QWidget>
	#include <QLabel>
	#include <QLineEdit>
	#include <QPushButton>
	#include <QGridLayout>

	class Login : public QWidget  {
	Q_OBJECT

	public:
	    Login();

	private:
	    QLabel *lUsuario, *lClave;
	    QLineEdit *leUsuario, *leClave;
	    QPushButton *pbAceptar;
	    QGridLayout *layout;

	private slots:
	    void slot_aceptar();
	};

	// login.cpp
	#include "login.h"

	Login::Login()  {
	    lUsuario = new QLabel("Usuario");
	    lClave = new QLabel("Clave");

	    leUsuario = new QLineEdit;
	    leClave = new QLineEdit;
	    leClave->setEchoMode(QLineEdit::Password);

	    pbAceptar = new QPushButton("Aceptar");

	    layout = new QGridLayout;
	    layout->addWidget(lUsuario, 0, 0);
	    layout->addWidget(lClave, 1, 0);
	    layout->addWidget(leUsuario, 0, 1, 1, 2);
	    layout->addWidget(leClave, 1, 1, 1, 2);
	    layout->addWidget(pbAceptar, 2, 2);

	    this->setLayout(layout);

	    connect(leClave, SIGNAL(returnPressed()), this, SLOT(slot_aceptar()));
	    connect(pbAceptar, SIGNAL(clicked()), this, SLOT(slot_aceptar()));
	}

	void Login::slot_aceptar()  {

	    if (leUsuario->text() == "admin" && leClave->text() == "1234")  {
	        this->close();
	    }
	    else  {
	        leUsuario->clear();
	        leClave->clear();
	    }
	}

 --->
