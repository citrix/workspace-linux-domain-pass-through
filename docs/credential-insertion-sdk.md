# Credential Insertion SDK

The Credential Insertion SDK allows you to insert a set of credentials into AM’s internal cache in order to be used to authenticate the user when launching an app/desktop.

The Credential Insertion SDK is a C/C++ library that must be consumed by external source code. The library exposes a set of functions that provide a convenient way to add and remove domain or smart card credentials to and from the AM’s internal cache.

Once credentials are made available to AM, it can then use them to authenticate the user in a SSO fashion.

## API functions

The CredInject API provides four functions to enable the use of SSO:

* `LogonSSOUser`
* `LogonSSOUserWithPin`
* `LogoffSSOUser`
* `ErrorDescription`

The function is available under the namespace `CitrixSSOnSDK`.

### LogonSSOUser

```
LOGONSSOUSER_ERROR_CODE LogonSsoUser	(const wchar_t *username, 
                                         const wchar_t *domain,
                                         const wchar_t *password);
```

This function is used to provide user credentials to SSO.

| Parameter | Description |
|---|---|
| `username` | The username |
| `domain` | The domain |
| `password` | The password |

| Return value | Description |
|---|---|
| `LOGONSSOUSER_OK` | Operation completed |
| `LOGONSSOUSER_INVALID_PARAMETER` | Invalid parameter passed to the function |
| `LOGONSSOUSER_INITIALIZATION_FAILED` | An error occurred initializing the SSO client |
| `LOGONSSOUSER_UNABLE_TO_CONNECT_TO_SSO` | Unable to connect to the SSO service (AM) |
| `LOGONSSOUSER_UNABLE_TO_SEND_REQUEST` | Unable to send the request to the SSO service |
| `LOGONSSOUSER_UNABLE_TO_RECEIVE_RESPONSE` | Unable to receive the response from the SSO service |
| `LOGONSSOUSER_INVALID_REQUEST_TYPE` | Invalid SSO request type |
| `LOGONSSOUSER_CONTAINER_FULL` | The SSO container is full and cannot store more credentials |
| `LOGONSSOUSER_SERVER_INTERNAL_ERROR` | An error has occurred in AM while processing the request |
| `LOGONSSOUSER_SERVER_IPC_ERROR` | An error has occurred during the IPC communication with the server (AM) |

### LogonSsoUserWithPin

```
LOGONSSOUSER_ERROR_CODE LogonSsoUserWithPin(const wchar_t *pin)
```

This function is used to provide smart card user credentials to SSO.

| Parameter | Description |
|---|---|
| `pin` | The smart card PIN |

| Return value | Description |
|---|---|
| `LOGONSSOUSER_OK` | Operation completed  |
| `LOGONSSOUSER_INVALID_PARAMETER` | Invalid parameter passed to the function |
| `LOGONSSOUSER_INITIALIZATION_FAILED` | An error occurred initializing the SSO client |
| `LOGONSSOUSER_UNABLE_TO_CONNECT_TO_SSO` | Unable to connect to the SSO service (AM) |
| `LOGONSSOUSER_UNABLE_TO_SEND_REQUEST` | Unable to send the request to the SSO service |
| `LOGONSSOUSER_UNABLE_TO_RECEIVE_RESPONSE` | Unable to receive the response from the SSO service |
| `LOGONSSOUSER_INVALID_REQUEST_TYPE` | Invalid SSO request type |
| `LOGONSSOUSER_CONTAINER_FULL` | The SSO container is full and cannot store more credentials |
| `LOGONSSOUSER_SERVER_INTERNAL_ERROR` | An error has occurred in AM while processing the request |
| `LOGONSSOUSER_SERVER_IPC_ERROR` | An error has occurred during the IPC communication with the server (AM) |

### LogoffSsoUser

```
int LogoffSsoUser()
```

This function removes the credentials of the current SSO user and restores the previous user’s credentials if available.

| Return value | Description |
|---|---|
| `LOGONSSOUSER_OK` | Operation completed  |
| `LOGONSSOUSER_INVALID_PARAMETER` | Invalid SSO parameter |
| `LOGONSSOUSER_INITIALIZATION_FAILED` | SSO client initialization failed |
| `LOGONSSOUSER_UNABLE_TO_CONNECT_TO_SSO` | Unable to connect to the SSO service |
| `LOGONSSOUSER_UNABLE_TO_SEND_REQUEST` | Unable to send the request to the SSO service |
| `LOGONSSOUSER_UNABLE_TO_RECEIVE_RESPONSE` | Unable to receive the response from the SSO service |
| `LOGONSSOUSER_INVALID_REQUEST_TYPE` | Invalid SSO request type (allowed types are ) |
| `LOGONSSOUSER_UNAUTHORIZED` | Trying to remove a set of credentials that was stored in SSO by AM itself |
| `LOGONSSOUSER_SERVER_INTERNAL_ERROR` | An error has occurred in AM while processing the request |
| `LOGONSSOUSER_SERVER_IPC_ERROR` | An error has occurred while establishing the IPC with AM |

### ErrorDescription

```
const wchar_t *ErrorDescription(LOGONSSOUSER_ERROR_CODE errorCode)
```

| Parameter | Description |
|---|---|
| `errorCode` | The error code to get the description of |

| Return value | Description |
|---|---|
| The error description | The error description string, or an “Unknown error” message if the error code is unknown |