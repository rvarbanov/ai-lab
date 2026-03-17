# Template: Modals / Dialogs

> Spec ref: Component Specification §12

## Confirmation Modal

```
+-------------------------------+
| [Modal Title]             [X] |
+-------------------------------+
| Are you sure you want to      |
| [action]? This cannot be      |
| undone.                       |
+-------------------------------+
| [Cancel]          [Confirm]   |
+-------------------------------+
```

## Form Modal

```
+-------------------------------+
| [Form Title]              [X] |
+-------------------------------+
| [Field 1 Input]               |
| [Field 2 Input]               |
| [Error: ...]                  |  ← validation state
+-------------------------------+
| [Cancel]          [Submit]    |
+-------------------------------+
```
