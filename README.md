# Salesforce Prettier for VSCode - Installation Guide.

Hi,this is a guide to help you configure a SFDX VSCode project with the Prettier Formatter.

## 1.Install Prettier Formatter.
Launch the following cmd:
```console 
npm install --save-dev prettier
npm install --save-dev prettier-plugin-apex
```
To format Apex install the prettier-apex-extension
```console
code --install-extension esbenp.prettier-vscode
```

## 2.Configure the files to be ignored by Prettier.
In the .prettierignore file in your project,paste:

```t
.sfdx
.localdevserver
.*ignore
*.*-meta.xml
*.sh
*.log
documentation/**
```

## 3.Configure your formatting style.
In the .prettierrc file in your project,paste:

```t
{
  "trailingComma": "none",
  "overrides": [
    {
      "files": "**/lwc/**/*.html",
      "options": {
        "tabWidth": 4,
        "parser": "lwc"
      }
    },
    {
      "files": "**/*.{cls,trigger,apex}",
      "options": {
        "apexInsertFinalNewline": true,
        "printWidth": 300,
        "tabWidth": 4
      }
    },
    {
      "files": "*.{cmp,page,component}",
      "options": {
        "parser": "html",
        "tabWidth": 4
      }
    }
  ]
}
```

## 4.Configure Your VSCode Prettier behaviour
In the settings.json file in the .vscode directory,put:
```t
{
  "editor.formatOnSave": true,
  "editor.formatOnType": true,
  "salesforcedx-vscode-apex.enable-semantic-errors": false,
  "editor.insertSpaces": true,
  "editor.detectIndentation": true,
  "files.insertFinalNewline": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode"
}
```

## 5.Format all the classes
In the package.json file add the following scripts that can be launched by terminal.
```t
"scripts": {
    "prettier:format:apex:all": "prettier --write \"**/*.{cls,trigger}\"",
    "prettier:format:visualforce:all": "prettier --write \"**/*.{page,}\"",
    "prettier:format:lwc:aura:all": "prettier --write '**/*.{html,js,css,cmp,component}'"
  },
```
These scripts format ALL the files of the selected type (cls,cmp,lwc).

The cmd to launch is:
```console 
npm run prettier:format:apex:all
```

## 6.NPM Install Error
In case you get error when launching the npm install commands, go into the VSCode package.json and revert the eslint version to :
```t
"eslint": "^8.57.0",
```

UPDATE*** The best way to solve the error is launching the following command for the installation:
```t
npm install --save-dev --save-exact prettier prettier-plugin-apex --legacy-peer-deps
```

## Documentation 
This guide is based on the work made by [von Jannis](https://lietzau-consulting.de/2021/09/prettier-sfdx-apex-visualforce-lwc/).


