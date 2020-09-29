## hello world
package.json部分关键内容如下（已省略其它）
```json
{
	// 扩展的激活事件
	"activationEvents": [
		"onCommand:extension.sayHello"
	],
	// 入口文件
	"main": "./src/extension",
	// 贡献点，vscode插件大部分功能配置都在这里
	"contributes": {
		"commands": [
			{
				"command": "extension.sayHello",
				"title": "Hello World"
			}
		]
	}
}
```
TODO
- [ ] 阅读vscode官方文档
- [ ] 阅读
http://blog.haoji.me/vscode-plugin-command-and-menu.html

## 命令
vscode 包含大量命令。调用系统自带的命令，一般使用` vscode.commands.executeCommand()`
查阅资料可知，`vscode.commands.executeCommand()`包含两个参数，一个是命令id，另一个是命令参数（可省略）。以下是样例。
```typescript
import * as vscode from 'vscode'
function  commentLine()
{
	vscode.commands.executeCommand('editor.action.addCommentLine');
}
```
### 命令URI
`editor.action.addCommentLine`命令 URI 是` command:editor.action.addCommentLine`.
### 创建新的命令
我们使用`vscode.commands.registerCommand`来注册一个新的命令。
```typescript
import * as vscode from 'vscode';

export function activate(context: vscode.ExtensionContext) {
  const command = 'myExtension.sayHello';

  const commandHandler = (name: string = 'world') => {
    console.log(`Hello ${name}!!!`);
  };

  context.subscriptions.push(vscode.commands.registerCommand(command, commandHandler));
}//command的值为myExtension.sayHello,commandHandler的值为一个函数。因此，我们注了一个命令。
```
为了能使用户能通过命令面板调用我们创建的命令。我们还需在`pakage.json`注册该命令
```json
{
  "contributes": {
    "commands": [
      {
        "command": "myExtension.sayHello",
        "title": "Say Hello"
      }
    ]
  }
}
```
为了能使用户能在命令面板直接调用我们的命令而不需要等待，我们还需要添加`activationEvent`到`pakage.json`.
```json
{
  "activationEvents": [
	  "onCommand:myExtension.sayHello"]
}
```
#### 控制命令面板何时显示命令
有时我们希望我们能控制我们的命令只在特定的时候显示，这时我们就要用到`when`。
```json
{
  "contributes": {
    "menus": {
      "commandPalette": [
        {
          "command": "myExtension.sayHello",
          "when": "editorLangId == markdown"//当编辑语言为markdown时显示命令。
        }
      ]
    }
  }
}
```

