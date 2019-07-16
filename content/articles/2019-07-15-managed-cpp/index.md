---
title: 'Managed C++: Clearing the C# myth'
author: Thomas Hounsell
type: post
date: 2019-07-15T09:00:00+00:00
url: /managed-cpp-in-longhorn
categories:
  - Research
  - Development

---

Reading up on Longhorn's development process, and you'll read a lot about how the shell or user interface was redeveloped using the .NET Framework, and many people infer that this meant using C#, including a number of Microsoft employees. This has then been blamed for the terrible performance of Longhorn and in particular, the rampant memory leaks it had.

It's time for a back to basics lesson on how the Longhorn shell was developed, to help dispell some of those common myths and get to the core of what went wrong in Longhorn's shell.

### Architecture

Let's take a step back for a moment and consider the shell improvements from a wider view. We know that the traditional `explorer.exe` shell has been steadily developed using native Windows APIs and C++ right from its inception. A cursory inspection of any Longhorn build will reveal that this remains largely unchanged. This is how builds for other architectures, such as AMD64, work and feel much like XP, with Windows Explorer working in very much the same way.

At this early stage, .NET was only supported on the 32-bit x86 platform. .NET Framework v2.0 would eventually add support for both IA-64 and AMD64, but this did not arrive ahead of Longhorn's development reset. While Longhorn for IA-64 and AMD64 both included _WoW64_ (Windows on Windows 64), which allowed 32-bit applications such as .NET to run, their `explorer.exe` shell was 64-bit, and you cannot mix architectures within the same process.

This betrays a little of how the "new" shell was implemented - it was not an independent new shell, but rather a (rather complex) plugin for Windows Explorer. The .NET Framework allows for the creation of COM components within managed libraries and so this is how it was implemented. Indeed, this is how many such changes had also been implemented in Whistler / Windows XP, albeit they were exclusively native C++ rather than using the .NET Framework. This is also how Longhorn can fallback gracefully to an XP-style experience - it attempts to load the new Longhorn extension via COM first, and if that fails, falls back to the XP-style COM experience. In the unusual event even that fails, you would end up with something akin to the "Classic" view, or Windows 2000 style.

### The Language?

So then, if they're using .NET, it's got to be C# right? It's _the_ .NET language. First-class support and the hot new thing Microsoft were pushing to developers at every opportunity. They even already had some experience of shipping a Windows component written in C# - Windows XP's Media Center was a purely managed C# affair for the most part, with only a small number of components written in C++.

For reasons we can only speculate, the Shell team did not use C# much, if at all, within the Longhorn shell. Instead, they used Microsoft's variant of C++ called *Managed C++*. This is related, but not quite the same as the more modern *C++/CLI*, which is Microsoft's second attempt at a C++ dialect for the .NET Framework, and probably one that was very much influenced by the painful experience of the Longhorn Shell.

There are a few probable reasons for this decision. One is that the C# language was very much in it's infancy. It is important to recall that at this early stage, C# was not the proven, mature language it is today. There was no support for generics, to take one example.

Furthermore, developers who had extensive experience with the language were few and mostly associated with the .NET team itself. Instead, what the Shell team did have an overabundance of was developers trained and highly experienced with C++. It would have likely seemed the wiser decision to limit the amount of on-the-job training by going with something that very much bridged the gap.

A third factor was likely the ease of interoperability with existing native code with Managed C++. The story in C# for interoperability is not horrible per se, but it was and still is from a developers point of view, more rigid and more work. In C#, you're required to use a Platform Invoke, or P/Invoke, that requires you to redefine the export in C#. For example, this export from the Windows SDK headers...

{{<highlight cpp>}}
INT ShellAboutW(HWND hWnd, LPCWSTR szApp, LPCWSTR szOtherStuff, HICON hIcon);
{{</highlight>}}

...would become this P/Invoke definition in C#:

{{<highlight csharp>}}
[DllImport("shell32.dll")]
static extern int ShellAbout(IntPtr hWnd, string szApp, string szOtherStuff, IntPtr hIcon);
{{</highlight>}}

Rather than go through and create all these redefinitions - which may also expose information that was limited before to private internal-only header files - using Managed C++ allowed MS to simply reference native functions in much the same way as they would in native C++, for example in this toy program (this is C++/CLI rather than MC++, which doesn't have the gcnew keyword):

{{<highlight cpp>}}
#include <string>
#include "windows.h"
#include "shellapi.h"

#pragma comment(lib, "shell32.lib")

using namespace System;

const char* show_shell_about()
{
    return ShellAbout(NULL, L"C++/CLI Sandbox", L"Hi from the Experience Longhorn project", NULL) == TRUE
        ? "True"
        : "False";
}

int main()
{
    auto result = show_shell_about();
    System::Console::Write("Result: ");
    System::Console::WriteLine(gcnew System::String(result));

    return 0;
}

{{</highlight>}}

This would have likely been considered a huge benefit to the Shell team which, with strict performance goals, were likely to be passing across the native / managed boundary quite frequently. Unlike C#, this also allows you to have a "mixed-mode" library or executable, which contains both unmanaged and managed code.

If you were to decompile the compiled version of the toy program above, you'd note some key differences from typical .NET executables. Using an IL decompiler, such as dnSpy, you'd notice that a lot of placeholder classes and structs that represent various structures defined in the Windows SDK headers. In a <Module> class, you'd find the methods that were in the global namespace, such as the `main()` and `show_shell_about()` from the toy program above. In here is our ShellAboutW() import stub, that dnSpy decompiles to the following C#:

{{<highlight csharp>}}
[SuppressUnmanagedCodeSecurity]
[DllImport("", CallingConvention = CallingConvention.StdCall, SetLastError = true)]
[MethodImpl(MethodImplOptions.Unmanaged)]
internal unsafe static extern int ShellAboutW(HWND__*, char*, char*, HICON__*);
{{</highlight>}}

The `show_shell_about()` method decompiles as so:

{{<highlight csharp>}}
internal unsafe static sbyte* show_shell_about()
{
  return ref (<Module>.ShellAboutW(null, (char*)(&<Module>.?A0x37975f1f.unnamed-global-1), (char*)(&<Module>.?A0x37975f1f.unnamed-global-0), null) != 1)
    ? ref <Module>.?A0x37975f1f.unnamed-global-3
    : ref <Module>.?A0x37975f1f.unnamed-global-2;
}
{{</highlight>}}

You can see that the strings have been pulled out into the executables' `.rdata` (read-only data) section and that .NET refers to them simply using automatically generated fields.

If you were to open this executable in a more typical decompiler, such as IDA Pro in PE mode, you'd see that unlike typical P/Invokes, a MC++ reference is also included in the imports table of the executable.

### Okay, but what does it all mean?

Well, Managed C++ came with some issues that Microsoft tried to rectify with C++/CLI. In particular, their overloading of the `new` keyword made it more difficult as to which objects would be collected by the managed garbage collector, and which objects had to be cleaned up manually by the developer. The potential outcome of such confusion would be that some objects never got collected or cleaned up, introducing a memory leak. Certainly, it is quite possible to introduce memory leaks in purely managed code, though not in the same way, but it does strike me that this is possibly a major contributing factor to Longhorn's well documented problems in this area. It's also noteworthy that they made the C++/CLI changes in line with the .NET 2.0 / Visual Studio 2005 release, after the Longhorn reset.