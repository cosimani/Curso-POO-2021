.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 07 - POO 2021
===================
(Fecha: 8 de abril)


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

**Ejercicio 10**

- Cuando el valor del QSlider se modifique, colocar como título de la ventana el mismo valor (de 0 a 100). 
	

**Ejercicio 11**

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


