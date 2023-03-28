Title: Paket Restore Failed with code 137
Published: 2023-01-03
Tags: 
    - F#
    - .NET
    - Paket
    - SAFE Stack

---

This morning I thought I'd give learning the [SAFE Stack](https://safe-stack.github.io) a go. As a long standing C# developer I've been seeing more and more language features come in to the language from F#, so it makes sense to me to see if those features a better fit in their natural environment.

I checked that I had the [correct dependencies](https://safe-stack.github.io/docs/quickstart/) for SAFE stack installed (.NET 6, Node), and then  installed the SAFE template 

`dotnet new -i SAFE.Template`

I created a new project with `dotnet new SAFE`, restored the tools required to build the project `dotnet tool restore`, and then ran the app with `dotnet run`

This resulted in the following error

```error MSB3073: The command "dotnet paket restore" exited with code 137.```

### What is Paket?

[Paket](https://fsprojects.github.io/Paket/) is an alternative dependency manager for .NET Projects, that has a few extra features over Nuget.

The principle reasoning behind Paket seems tro be that with Nuget, there is no way to see if a package is a direct dependency of a project, or a dependency that has been pulled in via a direct dependency, eg a _transitive dependency_, and that " If two packages reference conflicting versions of a package, NuGet will silently take the latest version."

Back to the error. Paket can be either installed globally on your machine, or local to a specific project. In the SAFE Stack template Paket is referenced as a local tool in the [dotnet-tools.json](https://github.com/SAFE-Stack/SAFE-template/blob/bfef529cc275aa972baee093d2e69e33562523cf/Content/default/.config/dotnet-tools.json) file, and is installed locally when you run `dotnet tool restore`.

Googling the error didn't glean much and there was nothing in Paket's issues list with that specific error code. There was a suggestion I found on twitter that it might be caused by a conflict between .NET 5 and .NET 6, and removing .NET 5 might fix the issue. It did not.

What i should have done was save myself a few minutes and  increased the verbosity of the dotnet run command with the `--verbosity diagnostic` switch. That gave a more detailed answer of `Failed to initialize CoreCLR, HRESULT: 0x80004005` and that was in the Paket issues list with [this answer](https://github.com/fsprojects/Paket/issues/4088#issuecomment-1083639950)

> please note paket 7.1.3 still requires .NET 3.1 installed, even when your project is on higher SDK versions. Otherwise it will give the `Failed to initialize CoreCLR, HRESULT: 0x80004005` error.

My Mac didn't have 3.1 on it, and installing it fixed the issue. Annoyingly, the dependencies for Paket does not list this as a requirement, the docs only say that 3.0 or higher is required.

### TL;DR;

At the time of writing, Paket has a dependency on the .NET 3.1 SDK. If you don't have that installed on your machine, Paket will not work.