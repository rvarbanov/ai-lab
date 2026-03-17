# Template: Multi-Page Workflow

> Spec ref: Output Format — multi-page flows

Use this pattern for any step-by-step flow (onboarding, wizard, checkout, etc.).

## Page 1: Start

```
+-------------------------------+
| Step 1 of N: [Step Name]      |
| [Progress: ●○○○○]             |
+-------------------------------+
| [Page 1 Content]              |
+-------------------------------+
|                  [Next →]     |
+-------------------------------+
```

## Page 2–(N-1): Middle

```
+-------------------------------+
| Step 2 of N: [Step Name]      |
| [Progress: ●●○○○]             |
+-------------------------------+
| [Page 2 Content]              |
+-------------------------------+
| [← Back]         [Next →]     |
+-------------------------------+
```

## Page N: Complete

```
+-------------------------------+
| Step N of N: [Step Name]      |
| [Progress: ●●●●●]             |
+-------------------------------+
| [Page N Content]              |
+-------------------------------+
| [← Back]         [Finish ✓]   |
+-------------------------------+
```

## Success / Confirmation

```
+-------------------------------+
|   [✓ Success Icon]            |
|   Flow complete!              |
|   [What happens next...]      |
|   [Go to Dashboard]           |
+-------------------------------+
```
