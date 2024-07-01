# Installation

On macos, the simplest way is always brew:

```
brew install archi-steam-farm
```

But not with some caveats, I don't know if it's just me or something wrong with this formulae, after I run `asf`, an error popped:

```
2024-07-01 17:05:58|dotnet-12202|FATAL|ASF|OnUnhandledException() System.DllNotFoundException: Unable to load shared library 'IOKit.framework/IOKit' or one of its dependencies. In order to help diagnose loading problems, consider setting the DYLD_PRINT_LIBRARIES environment variable:
dlopen(/opt/homebrew/Cellar/dotnet/8.0.4/libexec/shared/Microsoft.NETCore.App/8.0.4/IOKit.framework/IOKit.dylib, 0x0001): tried: '/opt/homebrew/Cellar/dotnet/8.0.4/libexec/shared/Microsoft.NETCore.App/8.0.4/IOKit.framework/IOKit.dylib' (no such file), '/System/Volumes/Preboot/Cryptexes/OS/opt/homebrew/Cellar/dotnet/8.0.4/libexec/shared/Microsoft.NETCore.App/8.0.4/IOKit.framework/IOKit.dylib' (no such file), '/opt/homebrew/Cellar/dotnet/8.0.4/libexec/shared/Microsoft.NETCore.App/8.0.4/IOKit.framework/IOKit.dylib' (no such file)
```

Apparently dotnet can't find some relevant dependencies. After some diggings, `IOKit.framework` is some library provided by MacOS, but `dotnet` search the wrong place or brew doesn't install `dotnet` right.

Anyway, `IOKit.framework` is located in the path: `/System/Library/Frameworks/IOKit.framework`, so we just soft-link it then the problem should be solved, let's do it:

```
ln -s /System/Library/Frameworks/IOKit.framework $HOMEBREW_PREFIX/Cellar/dotnet/8.0.4/libexec/shared/Microsoft.NETCore.App/8.0.4/IOKit.framework
```

> Remember to changed the version number if not `8.0.4`, else should be fine.

It turned out, not only `IOKit.framework` is missing but some other components. So the complete command is:

```
ln -s /System/Library/Frameworks/IOKit.framework $HOMEBREW_PREFIX/Cellar/dotnet/8.0.4/libexec/shared/Microsoft.NETCore.App/8.0.4/IOKit.framework

ln -s /System/Library/Frameworks/CoreFoundation.framework/ $HOMEBREW_PREFIX/Cellar/dotnet/8.0.4/libexec/shared/Microsoft.NETCore.App/8.0.4/CoreFoundation.framework

ln -s /System/Library/Frameworks/DiskArbitration.framework/ $HOMEBREW_PREFIX/Cellar/dotnet/8.0.4/libexec/shared/Microsoft.NETCore.App/8.0.4/DiskArbitration.framework
```

Viola! Enjoy Archi-Steam-Farm on MacOS via Homebrew.
