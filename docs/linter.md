# Linter Set Up Guide (Biome & SonarLint)

### What is a linter?

A linter is a static code analysis tool that helps developers identify and fix issues as they code. Linters help enforce coding standards, improve code quality, and reduce the likelihood of bugs in production.

---
We use 2 linters in our environment. 

| Type      | Linters |
| ----------- | ----------- |
| Frontend (JavaScript/TypeScript)      | Biome & SonarLint      | 
| Backend (C#)  | SonarLint        |

The setup guide is meant for VS Code and Visual Studio IDE. If you are using neither, please raise an issue to let us know to see how we can integrate linters for your IDE. 

:::info  Difference between Biome and SonarLint

SonarLint is an extension of SonarQube, which focuses on code quality and security. SonarLint also supports a range of languages.

Biome is primarily a unified formatter and linter that focuses on modern JS/TS ecosystems.

:::
--- 

## Biome setup

Biome is both a formatter and a linter tool. With this, Prettier is no longer necessary to format your code.

Benefits of Biome
- Extremely fast formatter (x35 faster than Prettier)
- Has 300+ inbuilt rules (and growing!)
- Minimal setup (works mostly out of the box with a few config file)
- Supports sorting of imports


Follow the steps below to set up Biome in your IDE.

1. Install the Biome VS Code Extension

   The extension can be found [here]. This extension is necessary so that it can automatically format and give inline suggestions from the VS Code IDE.

   (Add ad about installing VSIX)

2. Install Biome as a dependency in your project
   ```
   npm install --save-dev @biomejs/biome
   ```

3. Add the Biome configuration file into the root of the directory of the project
   ```
     {
  	"$schema": "https://biomejs.dev/schemas/1.9.4/schema.json",
  	"vcs": {
  		"enabled": false,
  		"clientKind": "git",
  		"useIgnoreFile": false
  	},
  	"files": {
  		"ignoreUnknown": false,
  		"ignore": []
  	},
  	"formatter": {
  		"enabled": true,
  		"indentStyle": "tab"
  	},
  	"organizeImports": {
  		"enabled": true
  	},
  	"linter": {
  		"enabled": true,
  		"rules": {
  			"recommended": true,
  			"correctness": {
  				"noUnusedImports": "warn",
  				"useExhaustiveDependencies": "warn"
  			},
  			"suspicious": {
  				"noExplicitAny": "warn"
  			}
  		}
  	},
  	"javascript": {
  		"formatter": {
  			"quoteStyle": "double"
  		}
  	}}
    ```

 (Add ad about overriding some of the rules)


4. Add the VS Code configuration file into your project

   Create a folder `.vscode` and place this VS Code configuration file `.settings,json`. Copy and paste this content below into the file.
   
    ```
        {
    	"editor.defaultFormatter": "biomejs.biome",
    	"editor.formatOnSave": true,
    	"editor.codeActionsOnSave": {
    		"quickfix.biome": "explicit"
    	}
    }
    ```

    This is necessary so that Biome can format your code and do simple fixes on save

--- 

## SonarLint setup (For VSCode)

To set up SonarLint, all you require is to install the extension into VSCode. **No other steps are required.**

**Install SonarLint extension**

You can find the extension [here], and add the extension to VS Code. You should now see SonarLint analyzing your code and flagging issues on your screen. 

## SonarLint setup (For Visual Studio)

To set up SonarLint, all you require is to install the extension into Visual Studio. **No other steps are required, however ensure all Visual Studio windows are closed first.**

**Install SonarLint extension**

You can find the extension [here]. Once you double-click the extension, it will install SonarLint extension into Visual Studio.
Once done, you should now see SonarLint analyzing your code and flagging issues on your screen. 