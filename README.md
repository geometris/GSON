{
  "name": "gson-debug",
  "displayName": "GSON Toolbox",
  "version": "0.1.202404031400",
  "publisher": "GeometrisLP",
  "description": "Geometris GSON extension for creating and debugging scripts using VS Code.",
  "author": {
    "name": "Geometris LP"
  },
  "license": "Commercial",
  "keywords": [
    "Geometris",
    "GSON",
    "Whereqube",
    "Scripting",
    "Telematics"
  ],
  "engines": {
    "vscode": "^1.81.0"
  },
  "icon": "images/gson-debug-icon.png",
  "categories": [
    "Debuggers",
    "Language Packs",
    "Programming Languages"
  ],
  "private": false,
  "repository": {
    "type": "git",
    "url": "https://github.com/geometris/GSON.git"
  },
  "bugs": {
    "url": "https://github.com/geometris/GSON/issues"
  },
  "scripts": {
    "compile": "tsc -p ./",
    "lint": "eslint src --ext ts",
    "typecheck": "tsc -p tsconfig.json --noEmit",
    "esbuild-base": "esbuild ./src/extension.ts --bundle --tsconfig=./tsconfig.json --external:vscode --format=cjs --platform=node --outfile=dist/extension.js",
    "watch": "npm run -S esbuild-base -- --sourcemap --sources-content=false --watch",
    "esbuild-web": "esbuild ./src/web-extension.ts --bundle --tsconfig=./tsconfig.json --external:vscode --format=cjs --platform=node --outfile=dist/web-extension.js",
    "watch-web": "npm run -S esbuild-web -- --sourcemap --sources-content=false --watch",
    "build": "npm run -S esbuild-base -- --sourcemap --sources-content=false && npm run -S esbuild-web -- --sourcemap --sources-content=false",
    "package": "vsce package",
    "package-dev": "vsce package --ignoreFile .vscodeignoredev --out gson-dev.vsix",
    "publish": "vsce publish",
    "publish-pre-release": "vsce publish --pre-release",
    "vscode:prepublish": "rimraf dist && npm run -S esbuild-base -- --minify && npm run -S esbuild-web -- --minify",
    "test": "npm run typecheck",
    "prettier": "prettier \"./**/*.{ts,html,css}\" --write"
  },
  "dependencies": {
    "@types/vscode-webview": "^1.57.0",
    "ajv": "^8.12.0",
    "axios": "^1.6.2",
    "comment-json": "^4.2.3",
    "fs-extra": "^11.2.0",
    "jsonc-parser": "^3.2.0",
    "serialport": "^11.0.0"
  },
  "devDependencies": {
    "@types/glob": "^7.2.0",
    "@types/mocha": "^9.1.0",
    "@types/node": "^14.14.37",
    "@types/vscode": "^1.66.0",
    "@typescript-eslint/eslint-plugin": "^5.17.0",
    "@typescript-eslint/parser": "^5.17.0",
    "@vscode/debugadapter": "^1.56.0",
    "@vscode/debugadapter-testsupport": "^1.56.0",
    "await-notify": "^1.0.1",
    "base64-js": "^1.5.1",
    "esbuild": "^0.14.54",
    "eslint": "^8.12.0",
    "events": "^3.3.0",
    "glob": "^7.2.0",
    "mocha": "^9.2.2",
    "path-browserify": "^1.0.1",
    "prettier": "^2.8.8",
    "rimraf": "^3.0.2",
    "typescript": "^4.6.3",
    "url": "^0.11.0",
    "vsce": "^2.15.0"
  },
  "main": "./dist/extension.js",
  "browser": "./dist/web-extension.js",
  "activationEvents": [
    "onLanguage:json",
    "onDebugResolve:gson",
    "onDebugDynamicConfigurations:gson",
    "onCommand:extension.gson-debug.getProgramName",
    "onUri"
  ],
  "workspaceTrust": {
    "request": "never"
  },
  "contributes": {
    "configuration": {
      "type": "object",
      "properties": {
        "gson.enableDev": {
          "readOnly": true,
          "type": "boolean",
          "default": false,
          "description": "Enable or disable the developer feature provided by GSON"
        },
        "gson.isNative": {
          "type": "boolean",
          "default": "true",
          "description": "Set type of devices sims are running on"
        },
        "gson.skyonicsAPIKey": {
          "type": "string",
          "default": "",
          "description": "Send command to native sims using Skyonics API Key"
        },
        "gson.twilioAPIKey": {
          "type": "string",
          "default": "",
          "description": "Send command through Twilio services, insert API Key"
        },
        "gson.twilioFrom": {
          "type": "string",
          "default": "",
          "description": "Send command through Twilio services, insert phone number"
        },
        "gson.twilioSID": {
          "type": "string",
          "default": "",
          "description": "Send command through Twilio services, insert string identifier"
        },
        "gson.defaultDevices": {
          "type": "array",
          "default": [],
          "description": "Default debug devices"
        }
      }
    },
    "menus": {
      "editor/title/run": [
        {
          "command": "extension.gson-debug.updateGsonSchema",
          "when": "resourceLangId == json || resourceLangId == jsonc",
          "group": "navigation@1"
        },
        {
          "command": "extension.gson-debug.assembleEditorContents",
          "when": "resourceLangId == json || resourceLangId == jsonc",
          "group": "navigation@2"
        },
        {
          "command": "extension.gson-debug.logDebugEditorContents",
          "when": "resourceLangId == json || resourceLangId == jsonc",
          "group": "navigation@3"
        },
        {
          "command": "extension.gson-debug.serialDebugEditorContents",
          "when": "resourceLangId == json || resourceLangId == jsonc",
          "group": "navigation@4"
        },
        {
          "command": "extension.gson-debug.uploadBySerialPort",
          "when": "resourceLangId == json || resourceLangId == jsonc",
          "group": "navigation@5"
        },
        {
          "command": "extension.gson-debug.debugLiveEditorContents",
          "when": "resourceLangId == json || resourceLangId == jsonc",
          "group": "navigation@6"
        },
        {
          "command": "extension.gson-debug.debugEditorContents",
          "when": "(resourceLangId == json || resourceLangId == jsonc) && config.gson.enableDev",
          "group": "navigation@7"
        },
        {
          "command": "extension.gson-debug.saveToCast",
          "when": "resourceLangId == json || resourceLangId == jsonc",
          "group": "navigation@8"
        },
        {
          "command": "extension.gson-debug.updateToCast",
          "when": "resourceLangId == json || resourceLangId == jsonc",
          "group": "navigation@9"
        },
        {
          "command": "extension.gson-debug.openFileFromCAST",
          "when": "(resourceLangId == json || resourceLangId == jsonc) && config.gson.enableDev",
          "group": "navigation@10"
        }
      ],
      "commandPalette": [
        {
          "command": "extension.gson-debug.updateGsonSchema",
          "when": "resourceLangId == json || resourceLangId == jsonc"
        },
        {
          "command": "extension.gson-debug.assembleEditorContents",
          "when": "resourceLangId == json || resourceLangId == jsonc"
        },
        {
          "command": "extension.gson-debug.logDebugEditorContents",
          "when": "resourceLangId == json || resourceLangId == jsonc"
        },
        {
          "command": "extension.gson-debug.serialDebugEditorContents",
          "when": "resourceLangId == json || resourceLangId == jsonc"
        },
        {
          "command": "extension.gson-debug.debugLiveEditorContents",
          "when": "resourceLangId == json || resourceLangId == jsonc"
        },
        {
          "command": "extension.gson-debug.debugEditorContents",
          "when": "(resourceLangId == json || resourceLangId == jsonc) && config.gson.enableDev"
        }
      ],
      "debug/variables/context": [
        {
          "command": "extension.gson-debug.toggleFormatting",
          "when": "debugType == 'gson' && debugProtocolVariableMenuContext == 'simple'"
        }
      ]
    },
    "commands": [
      {
        "command": "extension.gson-debug.updateGsonSchema",
        "title": "Get Schema",
        "category": "GSON Debug",
        "enablement": "!inDebugMode",
        "icon": "$(file-code)"
      },
      {
        "command": "extension.gson-debug.assembleEditorContents",
        "title": "Assemble File",
        "category": "GSON Debug",
        "enablement": "!inDebugMode",
        "icon": "$(gather)"
      },
      {
        "command": "extension.gson-debug.logDebugEditorContents",
        "title": "Log File Debugging",
        "category": "GSON Debug",
        "enablement": "!inDebugMode",
        "icon": "$(debug)"
      },
      {
        "command": "extension.gson-debug.serialDebugEditorContents",
        "title": "Serial Port Debugging",
        "category": "GSON Debug",
        "enablement": "!inDebugMode",
        "icon": "$(plug)"
      },
      {
        "command": "extension.gson-debug.uploadBySerialPort",
        "title": "Download to Device",
        "category": "GSON Debug",
        "enablement": "!inDebugMode",
        "icon": "$(cloud-upload)"
      },
      {
        "command": "extension.gson-debug.debugLiveEditorContents",
        "title": "Over the Air Debugging",
        "category": "GSON Debug",
        "enablement": "!inDebugMode",
        "icon": "$(server)"
      },
      {
        "command": "extension.gson-debug.toggleFormatting",
        "title": "Toggle between decimal and hex formatting"
      },
      {
        "command": "extension.gson-debug.saveToCast",
        "title": "Save to CAST",
        "category": "GSON Debug",
        "enablement": "!inDebugMode",
        "icon": "$(save-as)"
      },
      {
        "command": "extension.gson-debug.updateToCast",
        "title": "Update to CAST",
        "category": "GSON Debug",
        "enablement": "!inDebugMode",
        "icon": "$(edit)"
      },
      {
        "command": "extension.gson-debug.openFileFromCAST",
        "title": "Open from CAST (test)",
        "category": "GSON Debug",
        "enablement": "!inDebugMode",
        "icon": "$(edit)"
      },
      {
        "command": "extension.gson-debug.debugEditorContents",
        "title": "Test Debugging (dev)",
        "category": "GSON Debug",
        "enablement": "!inDebugMode",
        "icon": "$(debug-alt)",
        "when": "config.gson.enableDev && (resourceLangId == 'json' || resourceLangId == 'jsonc')"
      }
    ],
    "breakpoints": [
      {
        "language": "jsonc"
      },
      {
        "language": "json"
      }
    ],
    "debuggers": [
      {
        "type": "gson",
        "label": "GSON Debug",
        "languages": [
          {
            "id": "jsonc",
            "aliases": [
              "JSON with comments"
            ]
          },
          {
            "id": "json",
            "aliases": [
              "JSON"
            ]
          }
        ],
        "runtime": "./debugAdapter/gsonDebugAdapter.exe",
        "windows": {
          "runtime": "./debugAdapter/gsonDebugAdapter.exe"
        },
        "osx": {
          "runtime": "./debugAdapter/gsonDebugAdapter.exe"
        },
        "linux": {
          "runtime": "./debugAdapter/gsonDebugAdapter.exe"
        },
        "configurationAttributes": {
          "launch": {
            "required": [
              "program"
            ],
            "properties": {
              "program": {
                "type": "string",
                "description": "Absolute path to a GSON file.",
                "default": "${workspaceFolder}/${command:AskForProgramName}"
              },
              "stopOnEntry": {
                "type": "boolean",
                "description": "Automatically stop after launch.",
                "default": true
              },
              "logMode": {
                "type": "boolean",
                "description": "Enable log debugging.",
                "default": false
              },
              "serialPort": {
                "type": "string",
                "description": "Serial port to communicate with the interpreter",
                "default": "${command:AskForPortName}"
              },
              "baudRate": {
                "type": "number",
                "description": "Baud rate for the serial port",
                "baudRate": "${command:AskForBaudRate}"
              }
            }
          },
          "attach": {
            "required": [
              "program"
            ],
            "properties": {
              "program": {
                "type": "string",
                "description": "Absolute path to a GSON file.",
                "default": "${workspaceFolder}/${command:AskForProgramName}"
              },
              "stopOnEntry": {
                "type": "boolean",
                "description": "Automatically stop after attach.",
                "default": true
              },
              "logMode": {
                "type": "boolean",
                "description": "Enable log debugging.",
                "default": false
              },
              "serialPort": {
                "type": "string",
                "description": "Serial port to communicate with the interpreter",
                "default": "${command:AskForPortName}"
              },
              "baudRate": {
                "type": "number",
                "description": "Baud rate for the serial port",
                "baudRate": "${command:AskForBaudRate}"
              }
            }
          }
        },
        "initialConfigurations": [
          {
            "type": "gson",
            "request": "launch",
            "name": "Ask for json file name",
            "program": "${workspaceFolder}/${command:AskForProgramName}",
            "stopOnEntry": true
          },
          {
            "name": "GSON Debug: Launch on log mode",
            "type": "gson",
            "request": "launch",
            "program": "${workspaceFolder}/${command:AskForProgramName}",
            "logMode": true
          }
        ],
        "configurationSnippets": [
          {
            "label": "GSON Debug: Launch",
            "description": "A new configuration for 'debugging' a user selected GSON file.",
            "body": {
              "type": "gson",
              "request": "launch",
              "name": "Ask for json file name",
              "program": "^\"\\${workspaceFolder}/\\${command:AskForProgramName}\"",
              "stopOnEntry": true
            }
          },
          {
            "label": "GSON Debug: Launch with tcp port",
            "description": "A new configuration for 'debugging' a user selected GSON file.",
            "body": {
              "type": "gson",
              "request": "launch",
              "name": "Ask for json file name and debug with tcp port",
              "program": "^\"\\${workspaceFolder}/\\${command:AskForProgramName}\"",
              "stopOnEntry": true,
              "debugServer": 5420
            }
          },
          {
            "label": "GSON Debug: Launch via serial port",
            "description": "Start debugging session reading a specific serial port.",
            "body": {
              "type": "gson",
              "request": "launch",
              "name": "Select serial port and baud rate to start serial debugging",
              "program": "^\"\\${workspaceFolder}/\\${command:AskForProgramName}\"",
              "stopOnEntry": true,
              "debugServer": 5420
            }
          }
        ],
        "variables": {
          "AskForProgramName": "extension.gson-debug.getProgramName",
          "AskForPortName": "extension.gson-debug.getPortNames",
          "AskForBaudRate": "extension.gson-debug.getBaudRate",
          "AskForSerialNumber": "extension.gson-debug.getSerialNumber",
          "AskForPhoneNumber": "extension.gson-debug.getPhoneNumber"
        }
      }
    ]
  }
}
