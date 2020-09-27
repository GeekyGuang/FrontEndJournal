# 手把手教你配置webstorm

### 1. 配置终端为cmder或Git Bash
1. 打开设置，进入 Tools => Terminal
1. 将 Shell Path 改为bash.exe 的绝对路径(可用everything搜索)

![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1600053438432-98897206-03a3-4007-9073-4811eb6aca21.png#align=left&display=inline&height=878&margin=%5Bobject%20Object%5D&name=image.png&originHeight=878&originWidth=1227&size=83821&status=done&style=none&width=1227)
将 cmder 示符从 λ 改为 $（Git bash 用户请跳过此步骤），用 VSCode 打开文件 `C:\自己找路径\cmder\vendor\git-for-windows\etc\profile.d\git-prompt.sh`，将 λ 改为 $
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1600053691083-cf9d5dc6-e29e-46ab-8577-1b9f4da8c2c8.png#align=left&display=inline&height=569&margin=%5Bobject%20Object%5D&name=image.png&originHeight=569&originWidth=1289&size=92858&status=done&style=none&width=1289)
### 2. 配置git

1. 打开设置，进入 Version Control => Git
1. 将 Path to Git 改为 git.exe 的绝对路径，比如我的路径是 `C:\请自己找到对应的目录\cmder\vendor\git-for-windows\bin\git.exe`，如下图

![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1600053908954-4fe7388f-9a8a-45d1-b6ab-ab8ea79ea482.png#align=left&display=inline&height=878&margin=%5Bobject%20Object%5D&name=image.png&originHeight=878&originWidth=1227&size=101926&status=done&style=none&width=1227)
### 3. 让界面更美观

1. 将用不到的界面隐藏起来，操作方法：View => Appearance => 勾选如下

![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1600054488616-61ee52ac-7c72-45d0-bbb5-afaf98f84f1e.png#align=left&display=inline&height=381&margin=%5Bobject%20Object%5D&name=image.png&originHeight=381&originWidth=734&size=40356&status=done&style=none&width=734)

2. 安装 Material Theme UI 主题，操作方法：File => Settings => Plugins => Marketplace => 搜索 Material Theme UI 并安装

![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1600054937821-cda30b63-5b7f-4bdf-90de-20b46517ffae.png#align=left&display=inline&height=230&margin=%5Bobject%20Object%5D&name=image.png&originHeight=230&originWidth=442&size=11555&status=done&style=none&width=442)

3. 安装完成后进入 File => Settings => Appearance & Behavior => Material Theme，仿照下面的配置

![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1600055127111-57ca07f4-ca54-465a-a9a3-dec3103746aa.png#align=left&display=inline&height=771&margin=%5Bobject%20Object%5D&name=image.png&originHeight=771&originWidth=930&size=46989&status=done&style=none&width=930)
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1600055729281-be3e1703-ebbb-4a0c-a767-cf36cfe49517.png#align=left&display=inline&height=260&margin=%5Bobject%20Object%5D&name=image.png&originHeight=260&originWidth=834&size=17338&status=done&style=none&width=834)
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1600055825240-0f836692-7251-4995-81a9-8403a0753917.png#align=left&display=inline&height=458&margin=%5Bobject%20Object%5D&name=image.png&originHeight=458&originWidth=908&size=31022&status=done&style=none&width=908)
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1600056108271-7c15444b-97a1-481a-86d3-17152374694e.png#align=left&display=inline&height=878&margin=%5Bobject%20Object%5D&name=image.png&originHeight=878&originWidth=1227&size=79816&status=done&style=none&width=1227)

4. 安装Atom Material icons

![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1600056560670-377d7545-f6e2-487c-8a77-45c00b2262a9.png#align=left&display=inline&height=639&margin=%5Bobject%20Object%5D&name=image.png&originHeight=639&originWidth=866&size=57130&status=done&style=none&width=866)
### 4. 让代码更好看

1. 选择一个好看的字体配色，打开设置 => Editor => Color Scheme，选择一个你喜欢的配色，点击 OK，就可以预览这个配色了。我个人喜欢 Molokai 或者默认的 Darcula 配色。
1. 将字体设置为 JetBrains Mono、Source Code Pro 或者 Fira Code，方法为：打开 Editor => Font，然后如下图所示设置一下

![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1600056867258-62a66940-8ea3-42a0-be0c-b64e4044a70b.png#align=left&display=inline&height=878&margin=%5Bobject%20Object%5D&name=image.png&originHeight=878&originWidth=1227&size=115159&status=done&style=none&width=1227)

3. 注意把 Fallback 字体设置为 Microsoft Yahei 之类的中文字体。
3. 还有两处字体需要设置一下，分别是
   1. 进入 Editor => Color Scheme => Color Scheme Font，取消勾选 Use color scheme font instead of ...
   1. 进入 Editor => Color Scheme => Console Font，取消勾选 Use color scheme font instead of ...
   1. 点击保存，这样一来，所有字体就统一了。

![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1600056968146-a739abd7-2bc2-4f1d-ad19-c0dd0de21c33.png#align=left&display=inline&height=344&margin=%5Bobject%20Object%5D&name=image.png&originHeight=344&originWidth=813&size=28867&status=done&style=none&width=813)
### 5. 快捷键
#### 查看快捷键
**按2次shift**，弹出搜索框，搜索你要的操作就能看到快捷方式
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1600058925548-488e8fa9-e307-474a-96f3-b2e3cd86b2d0.png#align=left&display=inline&height=204&margin=%5Bobject%20Object%5D&name=image.png&originHeight=204&originWidth=903&size=15993&status=done&style=none&width=903)
第2种方式是查看菜单栏上对应的快捷方式
#### 修改快捷键
在setting里的keymap里搜索action名，修改快捷键
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1600059181235-e9c7c1b9-88c3-4be4-a301-6e128f522dc5.png#align=left&display=inline&height=878&margin=%5Bobject%20Object%5D&name=image.png&originHeight=878&originWidth=1227&size=71706&status=done&style=none&width=1227)
如果修改后提示快捷键有冲突，点击 Remove 即可把其他冲突的快捷键删除。
#### 常用快捷键设置

1. 查找文件，设置为 Ctrl + P（mac 用户自动将 Ctrl 脑补成 cmd 键吧）

![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1600059470648-2cf3dd78-9f38-46be-a4e7-cb23c4ab8396.png#align=left&display=inline&height=509&margin=%5Bobject%20Object%5D&name=image.png&originHeight=509&originWidth=912&size=37129&status=done&style=none&width=912)

2. 项目文件列表窗口，设置为 Alt + 1，这样任何时候你都可以显示或关闭项目文件列表
2. 终端窗口，设置为 Alt + 2，这样你任何时候都可以打开终端输入命令行了

![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1600059582702-84b82a67-04b0-451d-b792-b17f3b05da93.png#align=left&display=inline&height=489&margin=%5Bobject%20Object%5D&name=image.png&originHeight=489&originWidth=945&size=33961&status=done&style=none&width=945)

4. Git 窗口（上图中最下方的 Version Control 就是指 Git），设置为 Alt + 3（当然你可以改）
4. 关闭当前窗口，设置为 Ctrl + W，这是一个常用快捷键，设置完之后提示冲突，此时请点击 Remove

![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1600060068223-a7015ee2-9c9f-4065-9838-e72212bce924.png#align=left&display=inline&height=878&margin=%5Bobject%20Object%5D&name=image.png&originHeight=878&originWidth=1227&size=80766&status=done&style=none&width=1227)

6. 在 Keymap 里将 Main Menu => Edit => Extend Selection 设为 Alt + W，将 Main Menu => Edit => Shrink Selection 设为 Alt + Shift + W，这两个快捷键自己试试，非常有用。
6. 加强 Emmet

![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1600060321941-61c2f3c8-fe5f-4b8c-8deb-32dc6e5c0f77.png#align=left&display=inline&height=590&margin=%5Bobject%20Object%5D&name=image.png&originHeight=590&originWidth=1082&size=65280&status=done&style=none&width=1082)

8. 撤销与重做。撤销的默认快捷键是 Ctrl + Z，不需要改；但是重做的默认快捷键是 Ctrl + Shift + Z，建议在 keymap 里把给 redo 添加一个快捷键 Ctrl + Y（提示冲突就选择 Remove）

![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1600060410021-177ecd3e-c74f-4ef8-85dd-153add396265.png#align=left&display=inline&height=353&margin=%5Bobject%20Object%5D&name=image.png&originHeight=353&originWidth=917&size=27797&status=done&style=none&width=917)
### 6. 格式化代码
在任意 JS 文件，使用 Show Reformat File Dialog 功能
我们一般选择 Whole file 来格式化整个文件，但如果当前文件是别人的代码，你可能就要选择 Only VCS changed text，以防修改别的人代码，只格式化刚写的代码。
你可以在任何时候使用 Show Reformat File Dialog 功能重新弹出这个对话框进行修改配置。
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1600060709596-d409a4d8-467f-43f2-9908-32cd247ded34.png#align=left&display=inline&height=164&margin=%5Bobject%20Object%5D&name=image.png&originHeight=220&originWidth=546&size=11197&status=done&style=none&width=407)![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1600060721427-d3c85141-3615-4568-acf6-15ddd3b1b78f.png#align=left&display=inline&height=232&margin=%5Bobject%20Object%5D&name=image.png&originHeight=232&originWidth=406&size=14498&status=done&style=none&width=406)
使用 Reformat Code 功能（快捷键你要自己用 Shift Shift 搜索一下），就会立即格式化当前文件。
如果你对格式化后的文件不满意，那么

1. 在设置里选中 Editor => Code Style => TypeScript进行自定义（JavaScript同理）

![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1600060872669-e696f119-fc53-46fa-b6cb-14066ce3adfe.png#align=left&display=inline&height=562&margin=%5Bobject%20Object%5D&name=image.png&originHeight=562&originWidth=960&size=65644&status=done&style=none&width=960)
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1600060934718-99ed65b2-813f-4798-adbe-e9479e4b8084.png#align=left&display=inline&height=481&margin=%5Bobject%20Object%5D&name=image.png&originHeight=481&originWidth=1058&size=74015&status=done&style=none&width=1058)
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1600061017946-e5fc816d-b1cc-4223-bb1e-c70ab1900d1f.png#align=left&display=inline&height=481&margin=%5Bobject%20Object%5D&name=image.png&originHeight=481&originWidth=1179&size=54234&status=done&style=none&width=1179)
可选：个人建议把 JS、CSS、SCSS、TypeScript、HTML 代码缩进全改成 2、2、2，这样代码更紧凑。建议 JS 不加分号，TS 加分号。
### 7. 其他
开启以下功能（直接在 Shift Shift 后输入对应的英文即可开启，找不到不要来问我，因为这些选项都无关紧要）：

- Show tree indent guides，这个功能会在编辑器里添加竖线，方便代码对齐。
- Show method separators，这个功能会在每个方法上面添加横线，便于阅读代码。
- Breadcrumbs，搜索这个选项，然后选择 Dont't Show，用于隐藏面包屑（如下图），你也可以右键点击面包屑查看更多选项
![](https://cdn.nlark.com/yuque/0/2020/png/1753813/1600061464363-45b9cd82-fc80-4bbd-bbb9-b1367061fccc.png#align=left&display=inline&height=36&margin=%5Bobject%20Object%5D&originHeight=36&originWidth=637&size=0&status=done&style=none&width=637)面包屑
- Show CSS color preview as background，我个人喜欢开启这个功能

关闭以下功能（直接在 Shift Shift 后输入对应的英文即可关闭，找不到不要来问我，因为这些选项都无关紧要）：

- Show gutter icons，关闭此功能可能让编辑器更简洁

一些可能用到的功能

- Soft wrap，用于折行









