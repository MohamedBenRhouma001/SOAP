# Currency Converter SOAP Service

This Spring Boot application provides a SOAP-based service for performing currency conversion operations.

## Prerequisites
- Java Runtime Environment version 17 or later
- Maven build system version 3.6.0 or later

## Installation
1. Clone the project from Git or extract it from an archive.
2. Navigate to the project root directory:
   ```bash
   cd currency-converter-service
   ```
3. Build the project to generate Java classes from the XML schema:
   ```bash
   mvn clean install
   ```
   This will generate the Java entities `ConvertCurrencyRequest` and `ConvertCurrencyResponse` under `src/main/java/com/example/currency`.

## Running the Application
Start the application using:
```bash
mvn spring-boot:run
```
The WSDL interface for the service will be available at:
```bash
http://localhost:8080/ws/currencyConverter.wsdl
```

## Functional Testing
You can interact with the SOAP service using tools like SoapUI or Postman.

### Example SOAP Request
```xml
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:cur="http://example.com/currency">
    <soapenv:Header/>
    <soapenv:Body>
        <cur:ConvertCurrencyRequest>
            <cur:fromCurrency>USD</cur:fromCurrency>
            <cur:toCurrency>EUR</cur:toCurrency>
            <cur:amount>100</cur:amount>
        </cur:ConvertCurrencyRequest>
    </soapenv:Body>
</soapenv:Envelope>
```

### Expected Response
```xml
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/">
    <soapenv:Body>
        <cur:ConvertCurrencyResponse xmlns:cur="http://example.com/currency">
            <cur:convertedAmount>90.0</cur:convertedAmount>
        </cur:ConvertCurrencyResponse>
    </soapenv:Body>
</soapenv:Envelope>
```

### Testing with SoapUI
1. Create a new SOAP project in SoapUI.
2. Specify the WSDL URL: `http://localhost:8080/ws/currencyConverter.wsdl`.
3. Send a `ConvertCurrencyRequest` with test values (e.g., USD to EUR, amount 100).

### Testing with Postman
1. Configure an HTTP POST request to: `http://localhost:8080/ws`.
2. In the "Body" tab, select `raw` and set the type to `XML`.
3. Paste the example SOAP request XML and send it.

## Project Structure
- `pom.xml`: Defines Maven dependencies and configures the JAXB2 plugin for XML-to-Java binding.
- `src/main/resources/currency-converter.xsd`: XSD file specifying the structure of SOAP messages.
- `src/main/java/com/example/currency/CurrencyConverterApplication.java`: Main entry point of the application.
- `src/main/java/com/example/currency/endpoint/CurrencyConverterEndpoint.java`: Exposes the SOAP service endpoints.
- `src/main/java/com/example/currency/config/WebServiceConfig.java`: Configures the web service using Spring-WS.
- `src/main/resources/application.properties`: Centralized application configuration.

## Packaging
To package the project into a compressed archive:
- **Windows**: Right-click the `currency-converter-service` folder, then select "Send to > Compressed (zipped) folder".
- **macOS/Linux**: Run the following command from the parent directory of the project:
  ```bash
  zip -r currency-converter-service.zip currency-converter-service
  ```