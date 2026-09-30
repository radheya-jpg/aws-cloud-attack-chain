# MITRE ATT&CK Mapping

| Technique | Name | Activity |
|---|---|---|
| T1530 | Data from Cloud Storage | Credentials accessed from S3 |
| T1552.001 | Credentials In Files | Credentials stored in the exposed object |
| T1078.004 | Valid Accounts: Cloud Accounts | Stolen `dev-user` credentials used |
| T1548.005 | Temporary Elevated Cloud Access | Administrative role assumed |
| T1087.004 | Account Discovery: Cloud Account | `iam:ListUsers` executed |

## Notes

`T1552.001` is used for the exposed credentials file because the secret was stored in a file/object. `T1552.005` refers specifically to cloud instance metadata and is not the best fit for this scenario.

The ATT&CK mappings describe the behavior observed in this lab and are not intended to imply that each individual API call is malicious on its own.
