# Kibana Investigation

## 1. Start with AssumeRole

```text
eventName: "AssumeRole"
```

The goal was to identify unexpected role assumptions and inspect:

- source principal
- target role
- role session name
- event time
- source IP
- AWS region

The lab showed `dev-user` assuming `admin-role` using the session name:

```text
attacker-session
```

## 2. Trace the activity before the role assumption

```text
userIdentity_userName: "dev-user"
AND eventSource: "s3.amazonaws.com"
```

This was used to identify S3 activity performed by `dev-user`.

Relevant events:

```text
ListObjectsV2
GetObject
```

The `GetObject` event pointed to the exposed credentials object.

## 3. Check activity after escalation

```text
eventName: "ListUsers"
```

The event was associated with the assumed administrative role.

This connected the initial S3 access to the later IAM enumeration.

## Investigation Chain

```text
S3 GetObject
      ↓
dev-user
      ↓
AssumeRole
      ↓
admin-role
      ↓
ListUsers
```
