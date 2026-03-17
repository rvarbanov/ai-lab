# Template: Email Verification

> Spec ref: Component Specification §8 (registration flow step)

```
+-------------------------------+
|   Enter Verification Code     |
+-------------------------------+
| Sent to: user@example.com     |
|                               |
| [Code Input: _ _ _ _ _ _]     |
| [Resend Code]  [Submit]       |
|                               |
| [Error: Invalid code]         |  ← error state
+-------------------------------+
```
