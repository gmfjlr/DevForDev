---
layout: documentation
category: CSharp
title: Coding Conventions
order: 2
---

Please visit [C# Coding Conventions (C# Programming Guide)](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/inside-a-program/coding-conventions/)

### Coding conventions serve the following purposes:

  - They create a consistent look to the code, so that readers can focus on content, not layout.
  - They enable readers to understand the code more quickly by making assumptions based on previous experience.
  - They facilitate copying, changing, and maintaining the code.
  - They demonstrate C# best practices.

The guidelines in this topic are used by Microsoft to develop samples and documentation.

### Naming Conventions

  - In short examples that do not include using directives, use namespace qualifications. If you know that a namespace is imported by default in a project, you do not have to fully qualify the names from that namespace. Qualified names can be broken after a dot (.) if they are too long for a single line, as shown in the following example: 

```csharp
    var currentPerformanceCounterCategory = new System.Diagnostics.PerformanceCounterCategory();
```

  - You do not have to change the names of objects that were created by using the Visual Studio designer tools to make them fit other guidelines.
