Translating by Xuanwo

LFCS系列第二讲：如何安装和使用vi/m全功能文字编辑器
================================================================================
几个月之前，Linux基金会启动了LFCS(Linux Foundation Certified Sysadmin，Linux基金会认证系统管理员)认证来帮助遍布全世界的人们获得其在处理Linux系统管理任务上能力的认证。这些能力包括系统支持，第一手的故障诊断及维护再加上智能决策——知道何时向上游维护团队提出问题。

![Learning VI Editor in Linux](http://www.tecmint.com/wp-content/uploads/2014/10/LFCS-Part-2.png)

Learning VI Editor in Linux

请观看下面关于Linux基金会认证计划的演示：

<embed src="http://static.video.qq.com/TPout.swf?vid=l0163eohhs9&auto=0" allowFullScreen="true" quality="high" width="480" height="400" align="middle" allowScriptAccess="always" type="application/x-shockwave-flash"></embed>

本文是覆盖这个参加LFCS认证考试的所必需的范围和能力的十个教程的第二讲，我们将会介绍基础文件操作并理解vi/m编辑器下的模式。

### 使用vi/m进行基础文件编辑操作 ###

Vi是第一个为Unix编写的全屏文字编辑器。尽管它致力于变得小而简单，但是对于只用过图形界面文字编辑器的人来说，比方说NotePad++或者gedit，学会它可能会是一个重大的挑战。

要使用Vi，我们必须首先了解这个强大的程序运行的三种模式，以便于稍后我们学习它强大的文字编辑程序。

请注意，大多数现代的Linux发行版都会自带vi支持更多功能的变体——vim(“Vi improved”)。因此，在本教程中，vi和vim是可以交换的。

如果你的发行版没有安装vim，你可以通过下面的命令来安装它。

- Ubuntu和衍生版：aptitude update && aptitude install vim
- 基于Red Hat的发行版：yum update && yum install vim
- openSUSE：zypper update && zypper install vim

### 为什么我需要学习vi？ ###

学习vi至少有两个好理由。

1. vi总是可用的（不管你使用什么发行版），因为POSIX标准需要它。

2. vi不会消耗大量系统资源，而且允许我们手指不离开键盘就执行任何可以想象到的任务。

除此以外，vi还有一个内容覆盖广泛的内置手册，可以在程序启动之后通过`:help`调用。这个内置的帮助手册比vi/m的man pages包含了更多信息。

![vi Man Pages](http://www.tecmint.com/wp-content/uploads/2014/10/vi-man-pages.png)

vi Man Pages

#### 启动g vi ####

在你的命令行中输入`vi`来启动它。

![Start vi Editor](http://www.tecmint.com/wp-content/uploads/2014/10/start-vi-editor.png)

启动vi编辑器

然后按下`i`来进入插入模式，之后你就可以开始编辑了。另一种启动vi/m的方法是：

    # vi filename

这将打开一个以`filename`命名的新缓存区（之后将会有更多缓存区），稍后你可以将其保存到磁盘。

#### 理解 Vi 的模式 ####

1. 在普通模式下，vi允许用户浏览文件并输入vi命令（简短的，一个或多个大小写敏感的字母组合）。几乎所有命令都能在前面加上一个数字来表示重复执行的次数。

比方说，`yy`（或`Y`)复制当前行，而`3yy`（或`3Y`）复制当前以及接下来的两行（共三行）。无论是何种模式，我们随时可以通过按下`ESC`来进入普通模式。事实上，普通模式下所有键都被解析为命令而不是文本内容让很多初学者感到困惑。

2. 在Ex模式中，我们可以操作文件（包括保存当前文件和运行外部程序）。要进入该模式，我们必须从命令模式输入一个引号`:`，然后直接我们需要使用的Ex模式命令。运行结束后，vi将会自动返回普通模式。

3. 在插入模式中（通常使用`i`来进入这个模式），我们的输入都会变成文本。大多数按键都会以文本形式出现在屏幕上（一个重要的例外是`ESC`键，退出插入模式并返回到普通模式）。

![vi Insert Mode](http://www.tecmint.com/wp-content/uploads/2014/10/vi-insert-mode.png)

vi 插入模式

#### Vi 命令 ####

下表列出了常用的vi命令。文件编辑命令可以通过附加的惊叹号强制执行。（比如，`:q!`，不保存强行退出）

<table cellspacing="0" border="0">
  <colgroup width="290">
  </colgroup>
  <colgroup width="781">
  </colgroup>
  <tbody>
    <tr>
      <td bgcolor="#999999" height="19" align="LEFT" style="border: 1px solid #000000;"><b><span style="font-size: small;">&nbsp;命令</span></b></td>
      <td bgcolor="#999999" align="LEFT" style="border: 1px solid #000000;"><b><span style="font-size: small;">&nbsp;描述</span></b></td>
    </tr>
    <tr class="alt">
      <td height="18" align="LEFT" style="border: 1px solid #000000;"><span style="font-family: Courier New;">&nbsp;h 或 左方向键</span></td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;向左一个字符</td>
    </tr>
    <tr>
      <td height="18" align="LEFT" style="border: 1px solid #000000;"><span style="font-family: Courier New;">&nbsp;j 或 下方向键</span></td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;向下一行</td>
    </tr>
    <tr class="alt">
      <td height="18" align="LEFT" style="border: 1px solid #000000;"><span style="font-family: Courier New;">&nbsp;k 或 上方向键</span></td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;向上一行</td>
    </tr>
    <tr>
      <td height="18" align="LEFT" style="border: 1px solid #000000;"><span style="font-family: Courier New;">&nbsp;l (小写 L) 或 右方向键</span></td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;向右一个字符</td>
    </tr>
    <tr class="alt">
      <td height="18" align="LEFT" style="border: 1px solid #000000;"><span style="font-family: Courier New;">&nbsp;H</span></td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;跳转到页面顶部</td>
    </tr>
    <tr>
      <td height="18" align="LEFT" style="border: 1px solid #000000;"><span style="font-family: Courier New;">&nbsp;L</span></td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;跳转到页面底部</td>
    </tr>
    <tr class="alt">
      <td height="18" align="LEFT" style="border: 1px solid #000000;"><span style="font-family: Courier New;">&nbsp;G</span></td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;跳转到文件末尾</td>
    </tr>
    <tr>
      <td height="18" align="LEFT" style="border: 1px solid #000000;"><span style="font-family: Courier New;">&nbsp;w</span></td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;把一个字符移到右边</td>
    </tr>
    <tr class="alt">
      <td height="18" align="LEFT" style="border: 1px solid #000000;"><span style="font-family: Courier New;">&nbsp;b</span></td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;把一个字符移到左边</td>
    </tr>
    <tr>
      <td height="18" align="LEFT" style="border: 1px solid #000000;"><span style="font-family: Courier New;">&nbsp;0 (零)</span></td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;跳转到当前行开头</td>
    </tr>
    <tr class="alt">
      <td height="18" align="LEFT" style="border: 1px solid #000000;"><span style="font-family: Courier New;">&nbsp;^</span></td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;跳转到当前行第一个非空字符</td>
    </tr>
    <tr>
      <td height="18" align="LEFT" style="border: 1px solid #000000;"><span style="font-family: Courier New;">&nbsp;$</span></td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;跳转到当前行末尾</td>
    </tr>
    <tr class="alt">
      <td height="18" align="LEFT" style="border: 1px solid #000000;"><span style="font-family: Courier New;">&nbsp;Ctrl-B</span></td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;返回一屏</td>
    </tr>
    <tr>
      <td height="18" align="LEFT" style="border: 1px solid #000000;"><span style="font-family: Courier New;">&nbsp;Ctrl-F</span></td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;前进一屏</td>
    </tr>
    <tr class="alt">
      <td height="18" align="LEFT" style="border: 1px solid #000000;"><span style="font-family: Courier New;">&nbsp;i</span></td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;在光标位置插入</td>
    </tr>
    <tr>
      <td height="18" align="LEFT" style="border: 1px solid #000000;"><span style="font-family: Courier New;">&nbsp;I (大写 i)</span></td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;在光标当前行开头插入</td>
    </tr>
    <tr class="alt">
      <td height="18" align="LEFT" style="border: 1px solid #000000;"><span style="font-family: Courier New;">&nbsp;J (大写 j)</span></td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;将下一行加入当前行 (将下一行向上移动)</td>
    </tr>
    <tr>
      <td height="18" align="LEFT" style="border: 1px solid #000000;"><span style="font-family: Courier New;">&nbsp;a</span></td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;在当前光标位置后附加</td>
    </tr>
    <tr class="alt">
      <td height="18" align="LEFT" style="border: 1px solid #000000;"><span style="font-family: Courier New;">&nbsp;o (小写 O)</span></td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;在当前行之后创建一个空行</td>
    </tr>
    <tr>
      <td height="18" align="LEFT" style="border: 1px solid #000000;"><span style="font-family: Courier New;">&nbsp;O (大写 o)</span></td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;在当前行之前创建一个空行</td>
    </tr>
    <tr class="alt">
      <td height="18" align="LEFT" style="border: 1px solid #000000;"><span style="font-family: Courier New;">&nbsp;r</span></td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;替换当前光标位置的字符</td>
    </tr>
    <tr>
      <td height="18" align="LEFT" style="border: 1px solid #000000;"><span style="font-family: Courier New;">&nbsp;R</span></td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;在当前光标位置重写</td>
    </tr>
    <tr class="alt">
      <td height="18" align="LEFT" style="border: 1px solid #000000;"><span style="font-family: Courier New;">&nbsp;x</span></td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;删除当前光标位置的字符</td>
    </tr>
    <tr>
      <td height="18" align="LEFT" style="border: 1px solid #000000;"><span style="font-family: Courier New;">&nbsp;X</span></td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;删除当前光标位置之前（左）的字符</td>
    </tr>
    <tr class="alt">
      <td height="18" align="LEFT" style="border: 1px solid #000000;"><span style="font-family: Courier New;">&nbsp;dd</span></td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;剪切（相对后之后的粘贴）当前行</td>
    </tr>
    <tr>
      <td height="20" align="LEFT" style="border: 1px solid #000000;"><span style="font-family: Courier New;">&nbsp;D</span></td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;剪切当前光标位置到行末 (这个命令相当于 d$)</td>
    </tr>
    <tr class="alt">
      <td height="20" align="LEFT" style="border: 1px solid #000000;"><span style="font-family: Courier New;">&nbsp;yX</span></td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;给一个移动命令X，从当前光标位置复制对应数量字符，单词或者行</td>
    </tr>
    <tr>
      <td height="18" align="LEFT" style="border: 1px solid #000000;"><span style="font-family: Courier New;">&nbsp;yy or Y</span></td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;复制当前行</td>
    </tr>
    <tr class="alt">
      <td height="18" align="LEFT" style="border: 1px solid #000000;"><span style="font-family: Courier New;">&nbsp;p</span></td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;在当前光标位置粘贴（下一行）</td>
    </tr>
    <tr>
      <td height="18" align="LEFT" style="border: 1px solid #000000;"><span style="font-family: Courier New;">&nbsp;P</span></td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;在当前光标位置粘贴（前一行）</td>
    </tr>
    <tr class="alt">
      <td height="18" align="LEFT" style="border: 1px solid #000000;"><span style="font-family: Courier New;">&nbsp;. (句号)</span></td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;重复最后一个命令</td>
    </tr>
    <tr>
      <td height="18" align="LEFT" style="border: 1px solid #000000;"><span style="font-family: Courier New;">&nbsp;u</span></td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;撤销最后一个命令</td>
    </tr>
    <tr class="alt">
      <td height="18" align="LEFT" style="border: 1px solid #000000;"><span style="font-family: Courier New;">&nbsp;U</span></td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;撤销最后一行的最后一个命令。只要光标还在当前行，就会起作用。</td>
    </tr>
    <tr>
      <td height="18" align="LEFT" style="border: 1px solid #000000;"><span style="font-family: Courier New;">&nbsp;n</span></td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;找到下一个匹配串</td>
    </tr>
    <tr class="alt">
      <td height="18" align="LEFT" style="border: 1px solid #000000;"><span style="font-family: Courier New;">&nbsp;N</span></td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;找到上一个匹配串</td>
    </tr>
    <tr>
      <td height="18" align="LEFT" style="border: 1px solid #000000;"><span style="font-family: Courier New;">&nbsp;:n</span></td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;下一个文件；当多个文件被指定为编辑时，这个命令将会加载下一个文件。</td>
    </tr>
    <tr class="alt">
      <td height="20" align="LEFT" style="border: 1px solid #000000;">&nbsp;:e file</td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;在当前文件位置载入文件</td>
    </tr>
    <tr>
      <td height="20" align="LEFT" style="border: 1px solid #000000;">&nbsp;:r file</td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;插入当前光标位置（下一行）之后的文件内容</td>
    </tr>
    <tr class="alt">
      <td height="18" align="LEFT" style="border: 1px solid #000000;"><span style="font-family: Courier New;">&nbsp;:q</span></td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;不保存更改退出</td>
    </tr>
    <tr>
      <td height="20" align="LEFT" style="border: 1px solid #000000;">&nbsp;:w file</td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;将当前缓存区写入文件。 要附加到现有文件，使用 :w &gt;&gt; file。</td>
    </tr>
    <tr class="alt">
      <td height="18" align="LEFT" style="border: 1px solid #000000;"><span style="font-family: Courier New;">&nbsp;:wq</span></td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;写入当前文件内容并退出。相当于x!和ZZ</td>
    </tr>
    <tr>
      <td height="20" align="LEFT" style="border: 1px solid #000000;">&nbsp;:r! command</td>
      <td align="LEFT" style="border: 1px solid #000000;">&nbsp;执行命令并将输出插入到当前光标位置（下一行）</td>
    </tr>
  </tbody>
</table>

#### Vi 选项 ####

The following options can come in handy while running vim (we need to add them in our ~/.vimrc file).

    # echo set number >> ~/.vimrc
    # echo syntax on >> ~/.vimrc
    # echo set tabstop=4 >> ~/.vimrc
    # echo set autoindent >> ~/.vimrc

![vi Editor Options](http://www.tecmint.com/wp-content/uploads/2014/10/vi-options.png)

vi Editor Options

- set number shows line numbers when vi opens an existing or a new file.
- syntax on turns on syntax highlighting (for multiple file extensions) in order to make code and config files more readable.
- set tabstop=4 sets the tab size to 4 spaces (default value is 8).
- set autoindent carries over previous indent to the next line.

#### Search and replace ####

vi has the ability to move the cursor to a certain location (on a single line or over an entire file) based on searches. It can also perform text replacements with or without confirmation from the user.

a). Searching within a line: the f command searches a line and moves the cursor to the next occurrence of a specified character in the current line.

For example, the command fh would move the cursor to the next instance of the letter h within the current line. Note that neither the letter f nor the character you’re searching for will appear anywhere on your screen, but the character will be highlighted after you press Enter.

For example, this is what I get after pressing f4 in command mode.

![Search String in Vi](http://www.tecmint.com/wp-content/uploads/2014/10/vi-search-string.png)

Search String in Vi

b). Searching an entire file: use the / command, followed by the word or phrase to be searched for. A search may be repeated using the previous search string with the n command, or the next one (using the N command). This is the result of typing /Jane in command mode.

![Vi Search String in File](http://www.tecmint.com/wp-content/uploads/2014/10/vi-search-line.png)

Vi Search String in File

c). vi uses a command (similar to sed’s) to perform substitution operations over a range of lines or an entire file. To change the word “old” to “young” for the entire file, we must enter the following command.

    :%s/old/young/g

**Notice**: The colon at the beginning of the command.

![Vi Search and Replace](http://www.tecmint.com/wp-content/uploads/2014/10/vi-search-and-replace.png)

Vi Search and Replace

The colon (:) starts the ex command, s in this case (for substitution), % is a shortcut meaning from the first line to the last line (the range can also be specified as n,m which means “from line n to line m”), old is the search pattern, while young is the replacement text, and g indicates that the substitution should be performed on every occurrence of the search string in the file.

Alternatively, a c can be added to the end of the command to ask for confirmation before performing any substitution.

    :%s/old/young/gc

Before replacing the original text with the new one, vi/m will present us with the following message.

![Replace String in Vi](http://www.tecmint.com/wp-content/uploads/2014/10/vi-replace-old-with-young.png)

Replace String in Vi

- y: perform the substitution (yes)
- n: skip this occurrence and go to the next one (no)
- a: perform the substitution in this and all subsequent instances of the pattern.
- q or Esc: quit substituting.
- l (lowercase L): perform this substitution and quit (last).
- Ctrl-e, Ctrl-y: Scroll down and up, respectively, to view the context of the proposed substitution.

#### Editing Multiple Files at a Time ####

Let’s type vim file1 file2 file3 in our command prompt.

    # vim file1 file2 file3

First, vim will open file1. To switch to the next file (file2), we need to use the :n command. When we want to return to the previous file, :N will do the job.

In order to switch from file1 to file3.

a). The :buffers command will show a list of the file currently being edited.

    :buffers

![Edit Multiple Files](http://www.tecmint.com/wp-content/uploads/2014/10/vi-edit-multiple-files.png)

Edit Multiple Files

b). The command :buffer 3 (without the s at the end) will open file3 for editing.

In the image above, a pound sign (#) indicates that the file is currently open but in the background, while %a marks the file that is currently being edited. On the other hand, a blank space after the file number (3 in the above example) indicates that the file has not yet been opened.

#### Temporary vi buffers ####

To copy a couple of consecutive lines (let’s say 4, for example) into a temporary buffer named a (not associated with a file) and place those lines in another part of the file later in the current vi section, we need to…

1. Press the ESC key to be sure we are in vi Command mode.

2. Place the cursor on the first line of the text we wish to copy.

3. Type “a4yy to copy the current line, along with the 3 subsequent lines, into a buffer named a. We can continue editing our file – we do not need to insert the copied lines immediately.

4. When we reach the location for the copied lines, use “a before the p or P commands to insert the lines copied into the buffer named a:

- Type “ap to insert the lines copied into buffer a after the current line on which the cursor is resting.
- Type “aP to insert the lines copied into buffer a before the current line.

If we wish, we can repeat the above steps to insert the contents of buffer a in multiple places in our file. A temporary buffer, as the one in this section, is disposed when the current window is closed.

### Summary ###

As we have seen, vi/m is a powerful and versatile text editor for the CLI. Feel free to share your own tricks and comments below.

#### Reference Links ####

- [About the LFCS][1]
- [Why get a Linux Foundation Certification?][2]
- [Register for the LFCS exam][3]

--------------------------------------------------------------------------------

via: http://www.tecmint.com/vi-editor-usage/

作者：[Gabriel Cánepa][a]
译者：[译者ID](https://github.com/译者ID)
校对：[校对者ID](https://github.com/校对者ID)

本文由 [LCTT](https://github.com/LCTT/TranslateProject) 原创翻译，[Linux中国](https://linux.cn/) 荣誉推出

[a]:http://www.tecmint.com/author/gacanepa/
[1]:https://training.linuxfoundation.org/certification/LFCS
[2]:https://training.linuxfoundation.org/certification/why-certify-with-us
[3]:https://identity.linuxfoundation.org/user?destination=pid/1