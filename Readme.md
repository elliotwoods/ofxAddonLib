# Introduction

Settings for addons following the `ofx?????Lib` pattern when using the addon within Visual Studio. This mostly sets things like:

* Don't needlessly copy oF's DLL's to the addon folder.
* Make sure to build Release and Debug libs with different names, and in different locations (to avoid needing to Rebuild Solution).

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
    <Import Project="..\..\..\addons\ofxSquashLib\ofxSquash.props" />
```
Often you need to change this 4 times in the file (`Debug|x64`, `Release|x64`, `Debug|Win32`, `Release|Win32`)


# Notes

This property sheet should be above the openframeworksDebug.props / openframeworksRelease.props (we want to cancel out the Post-Build Event to xcopy the dll's into the Target App folder, and above means evaluated later).
