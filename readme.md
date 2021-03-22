# IncludePackageReferencesDuringMarkupCompilation Issue

This repo demonstrates an issue with the `IncludePackageReferencesDuringMarkupCompilation` property.  The issue is that if you exclude a package reference based on whether we're in the 'MarkupCompilation' phase (as indicated by a project name with the `wpftmp` suffix), `build` assets from that package reference will still be included in the build if `IncludePackageReferencesDuringMarkupCompilation` is true.

## To Reproduce

First build the `wpf-tmp-test` project.  You'll notice that a single warning is generated for the project.  This warning comes from a `.targets` file in the `my.package` NuGet package referenced by the project.

Next, `dotnet clean` and then `dotnet build -p:DemonstrateIssue=true`.  With the `DemonstrateIssue` property set, we'll set the `IncludePackageReferencesDuringMarkupCompiltion` property to `true`.  With this set to `true`, you'll now see two warnings - one from the `wpftmp` build, and one from the normal project build.