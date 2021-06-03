.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 20 - POO 2021
===================
(Fecha: 1 de junio)



Registrar eventos (logs)
^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: c

	bool AdminDB::registrar( QString evento )  {
	    QSqlQuery query( db );

	    bool exito = query.exec( "INSERT INTO registos (evento) VALUES ('" + evento + "')" );

	    qDebug() << query.lastQuery();
	    qDebug() << query.lastError();  // Devuelve un objeto de QSqlError

	    return exito;
	}


**Armando la clase AdminDB**

.. code-block:: c

	#ifndef ADMINDB_H
	#define ADMINDB_H

	#include <QObject>
	#include <QSqlDatabase>

	class AdminDB : public QObject
	{
	    Q_OBJECT
	public:
	    explicit AdminDB( QObject *parent = 0 );
	    ~AdminDB();

	    bool conectar( QString archivoSqlite );
	    QSqlDatabase getDB();
	    bool isConnected();
	    void mostrarTabla( QString tabla );

	private:
	    QSqlDatabase db;
	};

	#endif // ADMINDB_H

.. code-block:: c

	#include "admindb.h"
	#include <QDebug>
	#include <QSqlQuery>
	#include <QSqlRecord>

	AdminDB::AdminDB( QObject * parent ) : QObject( parent )  {
	    qDebug() << "Drivers disponibles:" << QSqlDatabase::drivers();

	    db = QSqlDatabase::addDatabase( "QSQLITE" );
	}

	AdminDB::~AdminDB()  {
	    if ( db.isOpen() )
	        db.close();
	}

	bool AdminDB::conectar( QString archivoSqlite )  {
	    db.setDatabaseName( archivoSqlite );

	    return db.open();
	}

	QSqlDatabase AdminDB::getDB()  {
	    return db;
	}

	bool AdminDB::isConnected()  {
	    return db.isOpen();
	}

	void AdminDB::mostrarTabla( QString tabla )  {
	    if ( this->isConnected() )  {
	        QSqlQuery query = db.exec( "SELECT * FROM " + tabla );

	        if ( query.size() == 0 || query.size() == -1 )
	            qDebug() << "La consulta no trajo registros";

	        while( query.next() )  {
	            QSqlRecord registro = query.record();  // Devuelve un objeto que maneja un registro (linea, row)
	            int campos = registro.count();  // Devuleve la cantidad de campos de este registro

	            QString informacion;  // En este QString se va armando la cadena para mostrar cada registro
	            for ( int i = 0 ; i < campos ; i++ )  {
	                informacion += registro.fieldName( i ) + ":";  // Devuelve el nombre del campo
	                informacion += registro.value( i ).toString() + " - ";
	            }
	            qDebug() << informacion;
	        }
	    }
	    else
	        qDebug() << "No se encuentra conectado a la base";
	}



Clase QTimer
^^^^^^^^^^^^

- Permite programar tareas de una sola ejecución o tareas repetitivas. 
- Conectamos la señal ``timeout()`` con algún slot.
- Con ``start()`` comenzamos y la señal ``timeout()`` se emitirá al terminar.


**Ejemplo (repetitivo):** Temporizador que cada 1000 mseg llamará a ``slot_update()``


.. code-block:: c

	QTimer * timer = new QTimer( this );
	connect( timer, SIGNAL( timeout() ), this, SLOT( slot_update() ) );
	timer->start( 1000 );
 

**Para una sola ejecución**

- Para temporizador de una sola ejecución usar ``setSingleShot(true)``
- El método estático ``QTimer::singleShot()`` nos permite la ejecución.


**Ejemplo:** Luego de 200 mseg se llamará a ``slot_update()``:


.. code-block:: c

	QTimer::singleShot( 200, this, SLOT( slot_update() ) );
	// donde this es el objeto que tiene definido el slot_update().
	



**Ejercicio 23**

- Diseñar una aplicación para una galería de fotos
- Debe tener una base con una tabla 'imagenes' que tenga las URLs de imágenes
- Un botón >> y otro << para avanzar o retroceder en la galería de fotos
- Se podrá navegar sobre las fotos que se descargarán desde internet




**Ejercicio 24**

- Usar QtDesigner
- Definir la clase Ventana que herede de QWidget
- Buscar una imagen de un fútbol con formato PNG (para usar transparencias).
- Ventana tendrá un formulario que pide al usuario:
	- Diámetro del fútbol (píxeles):
	- Velocidad (mseg para ir de lado a lado):
	- QPushButton para actualizar el estado.
- El fútbol irá golpeando de izquierda a derecha en Ventana.




