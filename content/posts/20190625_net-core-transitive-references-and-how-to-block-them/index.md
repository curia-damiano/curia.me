---
title: ".NET Core Transitive Dependencies and how to block them"
slug: "net-core-transitive-references-and-how-to-block-them"
draft: false
date: "2019-06-25T14:51:31Z"
categories:
  - "Software Development"
tags:
  - ".NET"
author: "Curia Damiano"
image: "img/DAL_BLL_UI.jpg"
---

In .NET Core, differently from .NET Framework, both Package and Project Dependencies are Transitive by default.

Let's suppose for example to have the following project structure:
* Project DAL:
  it references the Json.NET NuGet package and defines the class ClassDB;
* Project BLL:
  it references the DAL project;
* Project UI:
  it references the BLL project.

In this case, from the UI we will be able to access both the Json.NET package and the ClassDB class.
As you can guess, this is very dangerous, because it could let the developers to skip the architectural layers set up during design phase.

The way to change the default behavior is to add &lt;PrivateAssets&gt;all&lt;/PrivateAssets&gt; for each package/project dependency inclusion.
In this way, packages and classes used in the UI project when not directly imported would result in a compiler time error.

But adding this element for each inclusion of each project of our solution would be very annoying to implement, and above all would not be maintainable in case new project and dependencies are added.

Luckily, we can add a [Directory.Build.props](https://docs.microsoft.com/en-us/visualstudio/msbuild/customize-your-build?view=vs-2019#directorybuildprops-and-directorybuildtargets) file at the root level of our solution, with the following content:

```markup
<Project>
       <ItemDefinitionGroup>
              <PackageReference>
                     <PrivateAssets>all</PrivateAssets>
              </PackageReference>
              <ProjectReference>
                     <PrivateAssets>all</PrivateAssets>
              </ProjectReference>
       </ItemDefinitionGroup>
</Project>
```

In this way, the attribute is automatically set for all dependencies of our solution, and we don't need to maintain these references manually.
