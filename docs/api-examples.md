# API examples

The following are simple examples that show how to consume the Credential Insertion API.

## Example 1: Log on a user

The following code provides user credentials to SSO to log on a user.

```
bool DoLogonSsoUser(const std::wstring &username,
                    const std::wstring &domain,
                    const std::wstring &password)
{
    if (username.empty()
            || password.empty()
            || domain.empty())
    {
        // Credentials unavailable or incomplete.
        return false;
    }

    // Credentials are available, inject them to SSO.
    CitrixSSOnSDK::LOGONSSOUSER_ERROR_CODE result =
        CitrixSSOnSDK::LogonSsoUser(username.c_str(),
                                    domain.c_str(),
                                    password.c_str());

    // Check whether the credential injection was successful.
    if (result != CitrixSSOnSDK::LOGONSSOUSER_OK)
    {
        // Get the result description.
        const wchar_t *result_description = CitrixSSOnSDK::ErrorDescription(result);

        // Report the error.
        wprintf(L"LogonSsoUser() failed: %d %ls\n", result, result_description);

        return false;
    }

    // Success.
    return true;
}
```

## Example 2: Log on a user with a smart card

The following code provides user credentials to SSO to log on a user with a smart card.

```
bool DoLogonSsoUserWithPin(const std::wstring &pin)
{
    if (pin.empty())
    {
        // PIN unavailable.
        return false;
    }

    // PIN is available, inject it to SSO.
    CitrixSSOnSDK::LOGONSSOUSER_ERROR_CODE result =
        CitrixSSOnSDK::LogonSsoUserWithPin(pin.c_str());

    // Check whether the PIN injection was successful.
    if (result != CitrixSSOnSDK::LOGONSSOUSER_OK)
    {
        // Get the result description.
        const wchar_t *result_description = CitrixSSOnSDK::ErrorDescription(result);

        // Report the error.
        wprintf(L"LogonSsoUserWithPin() failed: %d %ls\n", result, result_description);

        return false;
    }

    // Success.
    return true;
}
```

## Example 3: Log off a user

This function performs a logoff from a SSO perspective, removing the user’s credentials from the system for the purposes of future SSO-based authorization. Existing authorized sessions can still be used.

```
void DoLogoffSsoUser()
{
    if (CitrixSSOnSDK::LogoffSsoUser() == LOGONSSOUSER_OK)
        printf("\nUser logged off\n");
    else
        printf("\nError logging off user\n");
}
```