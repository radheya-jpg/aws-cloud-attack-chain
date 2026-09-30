# Detection Opportunities

## 1. Public S3 Access

Detect buckets that allow public read access.

Relevant controls:

```text
S3 Block Public Access
AWS Config
```

A bucket containing credentials should never be publicly readable.

## 2. Unexpected AssumeRole

Example investigation query:

```text
eventName: "AssumeRole"
AND userIdentity_userName: "dev-user"
```

The useful signal is whether the principal normally assumes the target role.

Useful fields to investigate:

```text
userIdentity
requestParameters.roleArn
requestParameters.roleSessionName
sourceIPAddress
eventTime
```

## 3. IAM Enumeration After Role Assumption

```text
eventName: "ListUsers"
AND userIdentity_type: "AssumedRole"
```

`ListUsers` is not malicious by itself. It becomes more interesting when it occurs shortly after an unusual role assumption.

## 4. Correlate the Chain

A stronger detection would correlate:

```text
S3 GetObject
      ↓
Credential use
      ↓
AssumeRole
      ↓
IAM enumeration
```

This is more useful than alerting on any one API call in isolation.
