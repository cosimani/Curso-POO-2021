.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 13 - POO 2021
===================
(Fecha: 29 de abril)



**Algunas particularidades de QNetworkReply y QNetworkRequest**

- Para controlar los bytes que se van descargando se puede usar la señal de ``QNetworkReply``:

.. code-block:: c

	void downloadProgress( qint64 bytesRecibidos, qint64 bytesTotal )

- Los campos de la cabecera HTTP se pueden setear con el método de ``QNetworkRequest``:

.. code-block:: c

	void setRawHeader( const QByteArray & nombre, const QByteArray & valor )

	QNetworkRequest request;
	request.setUrl( QUrl( this->le->text() ) );
	request.setRawHeader( "User-Agent", "MiNavegador 1.0" );


**Ejercicio 19**

- Buscar el correspondiente valor de User-Agent para un navegador en Android y otro para PC
- Realizar una interfaz que permita colocar en un QLineEdit la url de una página web
- Validar que si el usuario no escribe el www, que lo agregue, y si no coloca https://, que lo agregue
- Realizar dos consultas a varias páginas web con ambos valores de User-Agent
- Mostrar en dos QTextEdit el código fuente de ambas páginas
- Comparar si los códigos son iguales y que un QLabel muestre "Iguales" o "Distintos" según corresponda

**Ejercicio 20**

- Crear una clase Barra para dar funcionalidad a una barra de progreso
- Que la barra tenga el siguiente aspecto:

.. figure:: images/clase12/progressbar.png

- Debe tener métodos para setear su valor en porcentaje
- Usar la señal de downloadProgress de QNetworkReply
- Crear una interfaz que tenga un QLineEdit para la URL y una Barra.
- Probarlo con alguna URL que pertenezca a un archivo de tamaño superior a 50MB


