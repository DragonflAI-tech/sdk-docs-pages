---
layout: default
title: LicenseStatus
has_children: true
parent: API (Android)
---

# LicenseStatus

`enum class LicenseStatus`

Represents the status of license verification

### Enum Values

| [NO_ACCOUNT_PROVIDED](no-account-provided.html) | Account credentials should be provided in the `AndroidManifest.xml` file or programmatically, via the `useAccount(...)` method. |
| [UNKNOWN](unknown.html) | License check not completed successfully at this point |
| [NO_LICENSE](no-license.html) | Licence check has completed, and the result is no current license to use the SDK. Contact us to verify your billing is set up correctly. |
| [LICENSED](licensed.html) | Licence check has completed, and the result is a valid license to use the SDK. |

