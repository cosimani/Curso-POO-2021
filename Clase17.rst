.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 17 - POO 2021
===================
(Fecha: 18 de mayo)



Consulta a la base de datos
^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: c

	QSqlDatabase db = QSqlDatabase::addDatabase( "QSQLITE" );

	db.setDatabaseName( "C:/Qt/db/test" ); 

	if ( db.open() )  {
	    QSqlQuery query = db.exec( "SELECT nombre, apellido FROM usuarios" );

	    while( query.next() )  {
	        qDebug() << query.value( 0 ).toString() << " " << query.value( 1 ).toString();
	    }
	}

	


**Ejemplo**: slot de la clase Login para que valide usuarios contra la base

.. code-block:: c

	void Login::slot_validar()  {
	    bool usuarioValido = false;

	    if ( adminDB->getDB().isOpen() )  {  
	        QSqlQuery * query = new QSqlQuery( adminDB->getDB() );

	        query->exec( "SELECT nombre, apellido FROM usuarios WHERE usuario='" + 
	        leUsuario->text() + "' AND clave='" + leClave->text() + "'" );

	        // Si los datos son consistentes, devolverá un único registro.
	        while ( query->next() )  {

	            QSqlRecord record = query->record();

	            // Obtenemos el número de la columna de los datos que necesitamos.
	            int columnaNombre = record.indexOf( "nombre" );
	            int columnaApellido = record.indexOf( "apellido" );

	            // Obtenemos los valores de las columnas.
	            qDebug() << "Nombre=" << query->value( columnaNombre ).toString();
	            qDebug() << "Apellido=" << query->value( columnaApellido ).toString();

	            usuarioValido = true;
	        }

	        if ( usuarioValido )  {
	            QMessageBox::information( this, "Conexión exitosa", "Válido" );
	        }
	        else  {
	            QMessageBox::critical( this, "Sin permisos", "Usuario inválido" );
	        }
	    }
	}


