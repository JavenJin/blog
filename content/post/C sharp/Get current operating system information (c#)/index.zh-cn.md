---
title: 获取当前操作系统信息（c#）
description: Get current operating system information (c#)
date: '2023-11-20'
categories:
    - C Sharp
tags:
    - C Sharp
---

# 获取当前操作系统信息（c#）

## System.Runtime.InteropServices.OSPlatform

```csharp
// Licensed to the .NET Foundation under one or more agreements.
// The .NET Foundation licenses this file to you under the MIT license.

using System.Diagnostics.CodeAnalysis;

namespace System.Runtime.InteropServices
{
    public readonly struct OSPlatform : IEquatable<OSPlatform>
    {
        public static OSPlatform FreeBSD { get; } = new OSPlatform("FREEBSD");

        public static OSPlatform Linux { get; } = new OSPlatform("LINUX");

        public static OSPlatform OSX { get; } = new OSPlatform("OSX");

        public static OSPlatform Windows { get; } = new OSPlatform("WINDOWS");

        internal string Name { get; }

        private OSPlatform(string osPlatform)
        {
            if (osPlatform == null) throw new ArgumentNullException(nameof(osPlatform));
            if (osPlatform.Length == 0) throw new ArgumentException(SR.Argument_EmptyValue, nameof(osPlatform));

            Name = osPlatform;
        }

        /// <summary>
        /// Creates a new OSPlatform instance.
        /// </summary>
        /// <remarks>If you plan to call this method frequently, please consider caching its result.</remarks>
        public static OSPlatform Create(string osPlatform)
        {
            return new OSPlatform(osPlatform);
        }

        public bool Equals(OSPlatform other)
        {
            return Equals(other.Name);
        }

        internal bool Equals(string? other)
        {
            return string.Equals(Name, other, StringComparison.OrdinalIgnoreCase);
        }

        public override bool Equals([NotNullWhen(true)] object? obj)
        {
            return obj is OSPlatform osPlatform && Equals(osPlatform);
        }

        public override int GetHashCode()
        {
            return Name == null ? 0 : StringComparer.OrdinalIgnoreCase.GetHashCode(Name);
        }

        public override string ToString()
        {
            return Name ?? string.Empty;
        }

        public static bool operator ==(OSPlatform left, OSPlatform right)
        {
            return left.Equals(right);
        }

        public static bool operator !=(OSPlatform left, OSPlatform right)
        {
            return !(left == right);
        }
    }
}
```

## System.Runtime.InteropServices.Architecture

```csharp
#region Assembly System.Runtime.InteropServices.RuntimeInformation, Version=6.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a
// C:\Program Files\dotnet\packs\Microsoft.NETCore.App.Ref\6.0.25\ref\net6.0\System.Runtime.InteropServices.RuntimeInformation.dll
#endregion

namespace System.Runtime.InteropServices
{
	//
	// Summary:
	//     Indicates the processor architecture.
	public enum Architecture
	{
		//
		// Summary:
		//     An Intel-based 32-bit processor architecture.
		X86 = 0,
		//
		// Summary:
		//     An Intel-based 64-bit processor architecture.
		X64 = 1,
		//
		// Summary:
		//     A 32-bit ARM processor architecture.
		Arm = 2,
		//
		// Summary:
		//     A 64-bit ARM processor architecture.
		Arm64 = 3,
		//
		// Summary:
		//     The WebAssembly platform.
		Wasm = 4,
		//
		// Summary:
		//     The S390x platform architecture.
		S390x = 5
	}
}
```

## System.Runtime.InteropServices.RuntimeInformation

```csharp
// Licensed to the .NET Foundation under one or more agreements.
// The .NET Foundation licenses this file to you under the MIT license.

using System.Reflection;

namespace System.Runtime.InteropServices
{
    public static partial class RuntimeInformation
    {
        private const string FrameworkName = ".NET";
        private static string? s_frameworkDescription;
        private static string? s_runtimeIdentifier;

        public static string FrameworkDescription
        {
            get
            {
                if (s_frameworkDescription == null)
                {
                    ReadOnlySpan<char> versionString = typeof(object).Assembly.GetCustomAttribute<AssemblyInformationalVersionAttribute>()?.InformationalVersion;

                    // Strip the git hash if there is one
                    int plusIndex = versionString.IndexOf('+');
                    if (plusIndex != -1)
                    {
                        versionString = versionString.Slice(0, plusIndex);
                    }

                    s_frameworkDescription = !versionString.Trim().IsEmpty ? $"{FrameworkName} {versionString}" : FrameworkName;
                }

                return s_frameworkDescription;
            }
        }

        /// <summary>
        /// Returns an opaque string that identifies the platform on which an app is running.
        /// </summary>
        /// <remarks>
        /// The property returns a string that identifies the operating system, typically including version,
        /// and processor architecture of the currently executing process.
        /// Since this string is opaque, it is not recommended to parse the string into its constituent parts.
        ///
        /// For more information, see https://docs.microsoft.com/dotnet/core/rid-catalog.
        /// </remarks>
        public static string RuntimeIdentifier =>
            s_runtimeIdentifier ??= AppContext.GetData("RUNTIME_IDENTIFIER") as string ?? "unknown";

        /// <summary>
        /// Indicates whether the current application is running on the specified platform.
        /// </summary>
        public static bool IsOSPlatform(OSPlatform osPlatform) => OperatingSystem.IsOSPlatform(osPlatform.Name);
    }
}
```

## Demo

```csharp
if (RuntimeInformation.IsOSPlatform(OSPlatform.Windows))
{
	// Windows
}
else if (RuntimeInformation.IsOSPlatform(OSPlatform.Linux) && RuntimeInformation.ProcessArchitecture == Architecture.X64)
{
	// linux64
}
```