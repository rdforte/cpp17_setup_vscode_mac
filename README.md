# C++11 Setup Notes for VSCode on a MAC.

### Step 1
Download *[VSCode](https://code.visualstudio.com)*

### Step 2
Navigate to your plugins in VSCode and download
1. *[C/C++](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools)*
2. *[Code Runner](https://marketplace.visualstudio.com/items?itemName=formulahendry.code-runner)*

### Step 3
While in VSCode. In your mac menu navigate to Terminal -> Configure Default Build Task...
You will get a drop down appear in VSCode with some options.
Select __clang++ build active file__
A __.vscode__ folder will appear in your active directory with a __tasks.json__ file.
Next you want to overwrite what you have in your tasks.json with the following:
```
{
	// See https://go.microsoft.com/fwlink/?LinkId=733558
	// for the documentation about the tasks.json format
	"version": "2.0.0",
	"tasks": [
	  {
		"type": "shell",
		"label": "clang++ build active file",
		"command": "/usr/bin/clang++",
		"args": [
		  "-std=c++17",
		  "-stdlib=libc++",
		  "-g",
		  "${file}",
		  "-o",
		  "${fileDirname}/${fileBasenameNoExtension}"
		],
		"options": {
		  "cwd": "${workspaceFolder}"
		},
		"problemMatcher": ["$gcc"],
		"group": {
		  "kind": "build",
		  "isDefault": true
		}
	  }
	]
  }
```

### Step 4
In VSCode hit __command ship p__ to bring up the vscode search bar.
You want to search for __C/C++: Edit Configurations(JSON)__
Select this.
Once you have selected this you will get a __c_cpp_properties.json__ file appear in your .vscode folder.
Replace what you have there with the following:
```
{
    "configurations": [
      {
        "name": "Mac",
        "includePath": ["${workspaceFolder}/**"],
        "defines": [],
        "macFrameworkPath": [
          "/Library/Developer/CommandLineTools/SDKs/MacOSX.sdk/System/Library/Frameworks"
        ],
        "compilerPath": "/usr/bin/clang",
        "cStandard": "c11",
        "cppStandard": "c++17",
        "intelliSenseMode": "clang-x64"
      }
    ],
    "version": 4
  }
```

### Last Step
Navigate to your __settings.json__ file in vscode and add the following:
```
"code-runner.executorMap": {
    "cpp": "cd $dir && g++ -std=c++17 $fileName -o $fileNameWithoutExt && $dir$fileNameWithoutExt",
  },
```
Now you should be able to build and run your cpp files by selectin __control option n__
