# Introduction

Settings for addons following the `ofx?????Lib` pattern when using the addon within Visual Studio. This mostly sets things like:

* Don't needlessly copy oF's DLL's to the addon folder.
* Make sure to build Release and Debug libs with different names, and in different locations (to avoid needing to Rebuild Solution).

# Notes

This property sheet should be above the openframeworksDebug.props / openframeworksRelease.props (we want to cancel out the Post-Build Event to xcopy the dll's into the Target App folder, and above means evaluated later).
