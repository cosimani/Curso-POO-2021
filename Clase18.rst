.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 18 - POO 2020
===================
(Fecha: 19 de mayo)


:Tarea para Clase 20:
	Se tomará un mini examen en computadora para resolver en 30 minutos

	Traer un programa con un login que valide usuario con la base de datos

	Será necesario: JADE (o similar) para creación de archivos .sqlite, creación de tablas, carga de datos, etc.

	También: MD5, material de las clases 15 y 16, Ejercicios 10 y 11, QSqlQuery, QSqlRecord, QSqlError, Registrar eventos (logs), INSERT INTO.




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






