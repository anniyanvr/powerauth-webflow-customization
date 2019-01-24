# Implementing the Data Adapter Interface

Data Adapter is used for connecting Web Flow to client backend systems. It allows to interact with backends for user authentication, SMS authorization, read additional data required for the operation as well as notify client backend about operation changes.   

## DataAdapter Interface

The interface methods are defined in the [DataAdapter interface](../powerauth-data-adapter/src/main/java/io/getlime/security/powerauth/app/dataadapter/api/DataAdapter.java):

- [authenticateUser](../powerauth-data-adapter/src/main/java/io/getlime/security/powerauth/app/dataadapter/api/DataAdapter.java#L43) - perform user authentication with remote backend based on provided credentials
- [fetchUserDetail](../powerauth-data-adapter/src/main/java/io/getlime/security/powerauth/app/dataadapter/api/DataAdapter.java#L52) - retrieve user details for given user ID
- [decorateFormData](../powerauth-data-adapter/src/main/java/io/getlime/security/powerauth/app/dataadapter/api/DataAdapter.java#L62) - retrieve operation form data and decorate it
- [formDataChangedNotification](../powerauth-data-adapter/src/main/java/io/getlime/security/powerauth/app/dataadapter/api/DataAdapter.java#L71) - method is called when operation form data changes to allow notification of client backends
- [operationChangedNotification](../powerauth-data-adapter/src/main/java/io/getlime/security/powerauth/app/dataadapter/api/DataAdapter.java#L80) - method is called when operation status changes to allow notification of client backends
- [generateAuthorizationCode](../powerauth-data-adapter/src/main/java/io/getlime/security/powerauth/app/dataadapter/api/DataAdapter.java#L89) - generate authorization code for authorization SMS message
- [generateSMSText](../powerauth-data-adapter/src/main/java/io/getlime/security/powerauth/app/dataadapter/api/DataAdapter.java#L100) - generate SMS text for authorization SMS message
- [sendAuthorizationSMS](../powerauth-data-adapter/src/main/java/io/getlime/security/powerauth/app/dataadapter/api/DataAdapter.java#L110) - send authorization SMS message

## Customizing Data Adapter

Following steps are required for customization of Data Adapter.

### 1. Implement Interface Methods

Consider which of the following methods need to be implemented in your project:

  - [authenticateUser](../powerauth-data-adapter/src/main/java/io/getlime/security/powerauth/app/dataadapter/api/DataAdapter.java#L43) (optional) - implementation is required in case any Web Flow operation needs to authenticate the user using a username/password login form
  - [fetchUserDetail](../powerauth-data-adapter/src/main/java/io/getlime/security/powerauth/app/dataadapter/api/DataAdapter.java#L52) (required) - provides information about the user (user ID and name) for the OAuth 2.0 protocol
  - [decorateFormData](../powerauth-data-adapter/src/main/java/io/getlime/security/powerauth/app/dataadapter/api/DataAdapter.java#L62) (optional) - implementation is required in case any Web Flow operation form data needs to be updated after authentication (e.g. add information about user bank accounts)
  - [formDataChangedNotification](../powerauth-data-adapter/src/main/java/io/getlime/security/powerauth/app/dataadapter/api/DataAdapter.java#L71) (optional) - implementation is required in case the client backends need to be notified about user input during an operation
  - [operationChangedNotification](../powerauth-data-adapter/src/main/java/io/getlime/security/powerauth/app/dataadapter/api/DataAdapter.java#L80) (optional) - implementation is required in case the client backends need to be notified about operation status changes
  - [generateAuthorizationCode](../powerauth-data-adapter/src/main/java/io/getlime/security/powerauth/app/dataadapter/api/DataAdapter.java#L89) (optional) - implementation is required in case any Web Flow operation needs to authorize the user using SMS authorization
  - [generateSMSText](../powerauth-data-adapter/src/main/java/io/getlime/security/powerauth/app/dataadapter/api/DataAdapter.java#L100) (optional) - implementation is required in case any Web Flow operation needs to authorize the user using SMS authorization
  - [sendAuthorizationSMS](../powerauth-data-adapter/src/main/java/io/getlime/security/powerauth/app/dataadapter/api/DataAdapter.java#L110) (optional) - implementation is required in case any Web Flow operation needs to authorize the user using SMS authorization

### 2. Implement the `DataAdapter` Interface

Implement the actual changes in Data Adapter so that it connects to an actual data source.

  - Clone project [powerauth-webflow-customization](https://github.com/wultra/powerauth-webflow-customization) from GitHub.
  - Update the `pom.xml` to add any required additional dependencies.
  - Create a proprietary client (+ client config) for your web services.
  - Implement the Data Adapter interface by providing your own implementation in the [DataAdapterService class](../powerauth-data-adapter/src/main/java/io/getlime/security/powerauth/app/dataadapter/impl/service/DataAdapterService.java). You can override the sample implementation.