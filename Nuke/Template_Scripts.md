You are here: [Compositing with Nuke](../nuke/nuke_intro.html) > [Configuring Nuke](configuring_nuke.html) > Template Scripts

# 模板脚本

您可以创建一个模板脚本，而不是每次启动Nuke或者选择 **File** > **New Comp** 或 **File** > **Close Comp**时都会加载一个空脚本。 例如，这可以保存查找表（LUT）设置和喜爱的节点排列。

## 创建和使用模板脚本

要创建和使用模板脚本：

1.  	创建要用作模板的脚本
2.  	选择 **File** > **Save Comp As**。导航到**~/.nuke**。 波浪符号（~）表示您的home目录, 句号（.）表示隐藏文件夹。
3.  	命名您的脚本为**template.nk**并单击保存。

下次启动Nuke或者选择 **File** > **New Comp** 或 **File** > **Close Comp**时, Nuke 将从 **~/.nuke/template.nk** 读取模版

> **TIP**: 如果您不确定主目录的位置，在Linux和Mac上，您可以打开终端窗口并键入echo $ HOME。 终端将返回您的主目录的路径。
>
> 在Windows上，您可以在HOME环境变量指向的目录下找到.nuke目录。 如果此变量未设置（这是常见的），则.nuke目录将位于由USERPROFILE环境变量指定的文件夹下。 要查看是否设置了HOME和USERPROFILE环境变量以及它们所在的位置，请在Windows资源管理器的地址栏中输入％HOME％或％USERPROFILE％。 如果设置了环境变量，将打开其指向的文件夹。 如果没有设置，您会收到错误。
>
> 以下是不同平台上路径名称的示例：
>
> **Linux**: /home/login name
> **Mac**: /Users/login name
> **Windows**: drive letter:\Documents and Settings\login name or drive letter:\Users\login name