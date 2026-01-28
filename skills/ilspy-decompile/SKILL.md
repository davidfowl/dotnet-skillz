---
name: ilspy-decompile
description: Decompiles .NET assemblies to C# source code using ILSpy. Use when the user needs to decompile DLLs, view decompiled source code, list types in assemblies, or generate projects from compiled .NET binaries.
allowed-tools: Bash(ilspycmd:*)
---

# .NET Assembly Decompilation with ilspycmd

## Quick start

```bash
# Install the tool (one-time setup)
dotnet tool install --global ilspycmd

# Decompile an assembly to stdout
ilspycmd MyLibrary.dll

# Decompile to an output folder
ilspycmd -o output-folder MyLibrary.dll
```

## Core workflow

1. Identify the assembly to decompile
2. Choose output format (C#, IL, or project)
3. Run ilspycmd with appropriate options
4. Review decompiled source code

## Commands

### Basic Decompilation

```bash
# Decompile to stdout
ilspycmd MyLibrary.dll

# Decompile to output directory
ilspycmd -o ./decompiled MyLibrary.dll

# Decompile as compilable project
ilspycmd -p -o ./project MyLibrary.dll

# Decompile with nested namespace folders
ilspycmd -p -o ./project --nested-directories MyLibrary.dll
```

### Targeted Decompilation

```bash
# Decompile a specific type
ilspycmd -t Namespace.ClassName MyLibrary.dll

# Decompile with specific C# version
ilspycmd -lv CSharp11_0 MyLibrary.dll

# Decompile with reference path for dependencies
ilspycmd -r ./dependencies MyLibrary.dll
```

### View IL Code

```bash
# Show IL code instead of C#
ilspycmd -il MyLibrary.dll

# Show IL for specific type
ilspycmd -il -t Namespace.ClassName MyLibrary.dll
```

### List Types

```bash
# List all classes
ilspycmd -l class MyLibrary.dll

# List interfaces
ilspycmd -l interface MyLibrary.dll

# List structs
ilspycmd -l struct MyLibrary.dll

# List enums
ilspycmd -l enum MyLibrary.dll

# List delegates
ilspycmd -l delegate MyLibrary.dll
```

### Generate PDB

```bash
# Generate PDB for debugging
ilspycmd -genpdb MyLibrary.dll
```

### Options

```bash
# Show version
ilspycmd -v

# Show help
ilspycmd -h

# Disable update check (useful for CI/automation)
ilspycmd --disable-updatecheck MyLibrary.dll

# Remove dead code
ilspycmd --no-dead-code MyLibrary.dll
```

## Example: Decompile NuGet package DLL

```bash
# Find and decompile a package DLL
ilspycmd ~/.nuget/packages/newtonsoft.json/13.0.1/lib/netstandard2.0/Newtonsoft.Json.dll

# Decompile to project for analysis
ilspycmd -p -o ./newtonsoft-src ~/.nuget/packages/newtonsoft.json/13.0.1/lib/netstandard2.0/Newtonsoft.Json.dll
```

## Example: Inspect specific type

```bash
# List all classes first
ilspycmd -l class MyLibrary.dll

# Then decompile the specific type you need
ilspycmd -t MyNamespace.MyClass MyLibrary.dll
```

## Example: Compare C# and IL

```bash
# View C# source
ilspycmd -t MyNamespace.MyClass MyLibrary.dll

# View IL code for same type
ilspycmd -il -t MyNamespace.MyClass MyLibrary.dll
```

## C# Language Versions

Available versions for `-lv` option:
- CSharp1, CSharp2, CSharp3, CSharp4, CSharp5, CSharp6, CSharp7, CSharp7_1, CSharp7_2, CSharp7_3
- CSharp8_0, CSharp9_0, CSharp10_0, CSharp11_0, CSharp12_0
- Latest, Preview
