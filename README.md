<p align="left">
<a href="https://travis-ci.org/Pleets/DronePHP"><img src="https://travis-ci.org/fermius/placetopay.svg?branch=master" alt="Build Status"></a>
</p>

# Implementación SOAP Service

Implementación de pago PSE con soap de PlacetoPay. Una copia de esta implementación ha sido subida al siguiente servidor a modo de demostración
http://darioriverat.com/placetopay/

## Instalación

Asegúrese que las siguientes extensiones están habilitadas en el archivo de configuración `php.ini`.

- intl
- soap

Para instalar las dependencias ejecute desde consola el siguiente comando en la raíz de la aplicación

```bash
php composer.phar install
```

Ejecute el siguiente script de MySQL para crear la base de datos y el schema

```sql
-- Base de datos de la aplicación
CREATE DATABASE placetopay;

USE placetopay;

-- Tabla para guardar resultado de la petición cuando es SUCCESS
CREATE TABLE PSETransactionResponse
(
	uniqueRequestId      VARCHAR(255)    NOT NULL PRIMARY KEY,
	transactionID        INTEGER         NOT NULL,
	sessionID            VARCHAR(32)     NOT NULL,
	returnCode           VARCHAR(30)     NOT NULL,
	trazabilityCode      VARCHAR(40)     NOT NULL,
	transactionCycle     INTEGER         NULL,
	bankCurrency         VARCHAR(3)      NULL,
	bankFactor           FLOAT(8,4)      NULL,
	bankURL              VARCHAR(255)    NULL,
	responseCode         INTEGER         NULL,
	responseReasonCode   VARCHAR(3)      NULL,
	responseReasonText   VARCHAR(255)    NULL
);
```

Finalmente asigne los permisos necesarios a la carpeta cache para que el usuario apache pueda escribir en ella.

```bash
chown apache cache
```

## Configuración

- Los datos de conexión de la base de datos se encuentran en el archivo `config/database.config.php`. Por defecto el usuario de la base de datos es root y la contraseña vacía.

## Test

La aplicación ha sido probada en las siguientes versiones de PHP

5.6, 7, 7.1, 7.2

Para ver el último resultado de pruebas unitarias visite el siguiente enlace

https://travis-ci.org/fermius/placetopay

Formulario de pagos PSE

/App/Pagos/index

Lista de bancos

/App/Soap/listaBancos

Lista de transacciones

/App/Pagos/listaTransacciones
