# Implementación SOAP Service

## Instalación

Asegúrese que las siguientes extensiones están habilitadas en el php.ini

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

## Test

Formulario de pagos PSE

/App/Pagos/index

Lista de bancos

/App/Soap/listaBancos