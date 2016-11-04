# Introduction

ofxAddonLib introduces a new pattern for working with addons in Visual Studio. It involves:

1. Putting all project settings required to use the addon into a `.props` file which Visual Studio can process automatically
2. Keeping all the addon source and header files in a seperate project in your solution

This has a number of advantages:

1. If an addon changes, you don't need to recreate any projects which use it
2. Build times can be quicker if you have multiple apps using the same addons
3. Addon developers can add complex build settings to their addons

# How to use an addon which uses ofxAddonLib pattern

1. Add the `ofx???.vcxproj` to your solution (`ofx???` = the name of your addon)
2. In `Property Manager` (open it from `View -> Other Windows -> Property Manager`), right click on your project to select `Add Existing Property Sheet...` and select the `ofx???/ofx???Lib/ofx_AddonName_.props` file
3. Right click on your project (e.g. 'mySketch') and select 'Add Reference...', and add a reference to `ofx???Lib`.

# Caveats

## Moving applications out of addon example folders

For applications inside addon folders (e.g. examples), Visual Studio will often store paths relatively inside the project and solution files. You may need to edit these yourself if you move the addon, for example:

### simpleExample.sln
```
Project("{8BC9CEB8-8B4A-11D0-8D11-00A0C91BC942}") = "ofxSquashLib", "..\ofxSquashLib\ofxSquashLib.vcxproj", "{FAA73572-FD12-41FA-8FBE-CB47482D2D87}"
```
needs to be changed to
```
Project("{8BC9CEB8-8B4A-11D0-8D11-00A0C91BC942}") = "ofxSquashLib", "..\..\..\addons\ofxSquash\ofxSquashLib\ofxSquashLib.vcxproj", "{FAA73572-FD12-41FA-8FBE-CB47482D2D87}"
```

### simpleExample.vcxproj
```
    <Import Project="..\ofxSquashLib\ofxSquash.props" />
```
needs to be changed to
```
    <Import Project="..\..\..\addons\ofxSquash\ofxSquashLib\ofxSquash.props" />
```
Often you need to change this 4 times in the file (`Debug|x64`, `Release|x64`, `Debug|Win32`, `Release|Win32`)


also...
```
    <ProjectReference Include="..\ofxSquashLib\ofxSquashLib.vcxproj">
```
needs to be changed to
```
    <ProjectReference Include="..\..\..\addons\ofxSquash\ofxSquashLib\ofxSquashLib.vcxproj">
```


# Notes

This property sheet should be above the openframeworksDebug.props / openframeworksRelease.props (we want to cancel out the Post-Build Event to xcopy the dll's into the Target App folder, and above means evaluated later).
