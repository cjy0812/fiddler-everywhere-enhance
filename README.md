# [耻辱柱（Hall of Shame)](./shame.md)

# 下载链接

## 最新版本

| 平台 | 链接 |
|----------|-------|
| Linux | https://api.getfiddler.com/linux/latest-linux |
| Windows | https://api.getfiddler.com/win/latest |
| Mac(Intel) | https://api.getfiddler.com/mac/latest-mac |
| Mac(Arm64) | https://api.getfiddler.com/mac-arm64/latest-mac|

## 旧版本

| 平台 | 链接 |
|----------|-------|
| Linux | https://downloads.getfiddler.com/linux/fiddler-everywhere-[版本号].AppImage |
| Windows | https://downloads.getfiddler.com/win/Fiddler%20Everywhere%20[版本号].exe |
| Mac(Intel)| https://downloads.getfiddler.com/mac/Fiddler%20Everywhere%20[版本号].dmg |
| Mac(Arm64) | https://downloads.getfiddler.com/mac-arm64/Fiddler%20Everywhere%20[版本号].dmg |

  > [!NOTE]
  > 在上述链接中，将 `[版本号]` 替换为你想要下载的版本号 <br>
  > 例如：https://downloads.getfiddler.com/win/Fiddler%20Everywhere%205.19.0.exe 用于下载 Windows 的 `5.19.0` 版本。
  
  > [!TIP] 
  > 你可以在这里找到可用版本列表：[版本历史记录](https://www.telerik.com/support/whats-new/fiddler-everywhere/release-history)

---

# 开始使用 - 补丁 / 增强适用于 v5.9.0 及以后版本（可能适用于所有版本）
  > [!IMPORTANT]
  > **对于 Windows 用户**:
  >  - 如果你使用的是 Fiddler Everywhere 5.16.0 或更早版本，请寻找 `libfiddler.dll` 而不是 `fiddler.dll`。
  >  - 在 5.17.0 及以后版本中，它被重命名为 `fiddler.dll`。

---

> [!TIP]
>  ## [自动补丁工具](https://github.com/msojocs/fiddler-everywhere-enhance/releases)
>  ## [你可以为 Windows & Linux 自动打补丁！](https://github.com/auto-yui-patch/fiddler-everywhere-patch-automated)

## 自动工具

1. 从 [release](https://github.com/msojocs/fiddler-everywhere-enhance/releases) 下载 AutoTool。
2. 运行 `fe-tool.exe -version latest` (Windows) 或 `fe-tool -version latest` (Linux)。
3. 工具完成后，输出文件将位于 `FiddlerEverywhere` 目录中。

## Windows

1. 删除 libfiddler.dll (对于 5.17.0+ 版本是 fiddler.dll)。
2. 访问 https://github.com/project-yui/Yui-patch/releases
3. 下载 `yui-fiddler-win32-x86_64-vx.x.x.dll`
4. - 如果你为 Fiddler Everywhere 5.16.0 或更早版本打补丁，将 `yui-fiddler-win32-x86_64-vx.x.x.dll` 重命名为 `libfiddler.dll`
   - 如果你为 Fiddler Everywhere 5.17.0 或更晚版本打补丁，将 `yui-fiddler-win32-x86_64-vx.x.x.dll` 重命名为 `fiddler.dll`
5. 将 `fiddler.dll` (对于 `5.16.0` 及更早版本是 `libfiddler.dll`) 移动到 Fiddler Everywhere 的 *根文件夹*
6. 复制 `resources\app\out\main.js` 为 `resources\app\out\main.original.js`
7. 按照下面的说明修改 `main.js` 文件。
8. 复制 `server/file` -> `Fiddler/resources/app/out/file`

## Linux

1. 删除 `libfiddler.so`。
2. 访问 https://github.com/project-yui/Yui-patch/releases
3. 下载 `yui-libfiddler-linux-x86_64-vx.x.x.so` 并将其重命名为 `libfiddler.so`
4. 将 `libfiddler.so` 移动到 fiddler 的根目录。
5. 复制 `resources/app/out/main.js` 为 `resources/app/out/main.original.js`
6. 按照下面的说明修改 `main.js` 文件。
7. 复制 `server/file` -> `Fiddler/resources/app/out/file`

> [!NOTE]
> 你可能需要自己重新编译 `libfiddler.so`。

## Mac 

1. 删除 `libfiddler.dylib` (对于 5.17.0+ 版本是 fiddler.dylib)，它位于 `Contents/Frameworks` 目录中。
2. 访问 https://github.com/project-yui/Yui-patch/releases
3. 下载 `yui-fiddler-mac-[架构]-vx.x.x.dylib`
4. - 如果你为 Fiddler Everywhere 5.16.0 或更早版本打补丁，将 `yui-fiddler-mac-[架构]-vx.x.x.dylib` 重命名为 `libfiddler.dylib`
   - 如果你为 Fiddler Everywhere 5.17.0 或更晚版本打补丁，将 `yui-fiddler-mac-[架构]-vx.x.x.dylib` 重命名为 `fiddler.dylib`
5. 将 `fiddler.dylib` (对于 `5.16.0` 及更早版本是 `libfiddler.dylib`) 移动到 `Contents/Frameworks` 目录。
6. 复制 `Resources/app/out/main.js` 为 `Resources/app/out/main.original.js`
7. 按照下面的说明修改 `main.js` 文件。
8. 复制 `server/file` -> `Contents/Resources/app/out/file`

> [!NOTE]
> 你可能需要自己重新编译 `fiddler.dylib` (对于 `5.16.0` 及更早版本是 `libfiddler.dylib`)。
>
> 你可能需要运行命令：`sudo codesign -s "-" --deep --force --verbose /Applications/Fiddler\ Everywhere.app`。 [issue#96](https://github.com/msojocs/fiddler-everywhere-enhance/issues/96#issuecomment-2814035393)

  ---

# 如何修改 `main.js`

1. 在文本编辑器中打开 `resources/app/out/main.js`
2. 打开并复制 `server/index.js` 的内容，然后将其附加到 `resources/app/out/main.js` 的开头。

# 修改 **名**、**姓** 和 **电子邮件** (附加功能)
如果你想更改默认的`名`、`姓`和`电子邮件`，可以编辑 `resources/app/out/file/identity.getfiddler.com/oauth/token.json`。
  - `token.json` 的内容：
    ```json
      {
        "id_token": "eyJhbGciOiJFUzI1NiIsImtpZCI6IjU4MDY4OTQzLWNlYmItNDY1OS1iNjZkLWZmZjY5NTg2NzA1ZCIsInR5cCI6IkpXVCJ9.eyJpYXQiOjE2OTU5MTE3ODcsImp0aSI6ImIwNWIxNjhiLTFiNjQtNDRlNy1iN2QzLWZiNWIzZDE3N2Y5YiIsInN1YiI6IjRmZGYzOWYzMmYyODRiMjhhMjFhYWFkMWYzNGI2OTk0IiwiZW1haWwiOiJqaXllY2FmZUBnbWFpbC5jb20iLCJpZGVudGl0aWVzIjpbeyJwcm92aWRlck5hbWUiOiJHb29nbGUiLCJwcm92aWRlclR5cGUiOiIifV0sImN1c3RvbTpmaXJzdF9uYW1lIjoiam9jcyIsImN1c3RvbTpsYXN0X25hbWUiOiJtc28iLCJjdXN0b206Y291bnRyeSI6IjgzIiwibmJmIjoxNjk1OTExNzg3LCJleHAiOjE2OTU5MTUzODcsImlzcyI6Imh0dHBzOi8vaWRlbnRpdHkuZ2V0ZmlkZGxlci5jb20vIiwiYXVkIjoiZmlkZGxlciJ9.9sLm19DExaTaraNtdJnTWUibua3toHENsTcDwxg6022rcHHshA0esnebks7WLWBAG7svYVyWkPWKDuHbB3syTA",
        "expires_in": 3539,
        "token_type": "Bearer",
        "user_info": {
          "id": "4fdf39f32f284b28a21aaad1f34b6994",
          "email": "user@gmail.com",
          "firstName": "first",
          "lastName": "last",
          "country": "83",
          "identities": [
            {
              "providerName": "Google"
            }
          ]
        }
      }
    ```
  - 在此 json 中，你可以通过替换相应的值来编辑 `email: user@gmail.com`、`firstName: first` 和 `lastName: last`。你也可以更改 `country` 和 `provider`。

> [!TIP]
> 更改这些值后，你可能需要退出并重新登录。

> [!CAUTION]
> - 如果你更改了上面 `token.json` 中的电子邮件，Fiddler Everywhere 会认为这是一个新用户，你的"已保存的快照"将无法供新用户（新电子邮件）使用。
> - 如果你想恢复这些快照，必须将电子邮件改回来。
> - 更改 `firstname`、`lastname`、`country`、`provider` 不会产生影响。

---

# 多语言支持

默认不支持，若要支持中文，请将`server/translate.js`复制到`resources\app\out\translate.js`

按<kbd>Ctrl+T</kbd>切换语言。

# 额外信息

[让我看看旧版](./v4.6.2/readme.md)

[让我看看更旧的版本](./old/DETAIL.MD)

---

# 其他

本项目 CDN 加速及安全防护由 Tencent EdgeOne 赞助：EdgeOne 提供长期有效的免费套餐，包含不限量的流量和请求，覆盖中国大陆节点，且无任何超额收费，感兴趣的朋友可以点击下面的链接领取。

[亚洲最佳CDN、边缘和安全解决方案 - Tencent EdgeOne](https://edgeone.ai/zh?from=github)
[![](https://edgeone.ai/media/34fe3a45-492d-4ea4-ae5d-ea1087ca7b4b.png)](https://edgeone.ai/zh?from=github)

## 免责声明
	
* readme使用AI翻译，请仔细甄别。
* 本仓库仅供技术学习交流使用，如有下载相关文件，请在学习后24小时内删除相关内容。
* 如果你觉得软件很好用，请购买官方正版：https://www.telerik.com/purchase/fiddler
* 切勿在 tb/pdd 等商城的非法渠道付费此软件。
* 如将本仓库教程/文件用于获利，那么：你妈死了。
* 请勿将本项目内容用于非法用途，使用者在使用时即视为对行为可能产生的任何不良后果负责。
* 由于传播、利用此工具所提供的信息而造成的任何直接或者间接的后果及损失，均由使用者本人负责，作者不为此承担任何责任。

## Disclaimer

* This repository is only for technical learning and communication. If you download related files, please delete the related content within 24 hours after learning.
* If you think the software is useful, please buy the official version: https://www.telerik.com/purchase/fiddler
* Do not pay for this software through illegal channels such as tb/pdd.
* If you use this repository tutorial/file for profit, then: your mother is dead.
* Please do not use the content of this project for illegal purposes. When using it, the user is deemed to be responsible for any adverse consequences that may arise from the behavior.
* Any direct or indirect consequences and losses caused by the dissemination and use of the information provided by this tool are the responsibility of the user himself, and the author does not assume any responsibility for this.
