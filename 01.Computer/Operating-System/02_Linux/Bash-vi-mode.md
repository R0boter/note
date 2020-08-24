# Bash的vi-mode

设置：`set -o vi`将这条命令加入bashrc

快捷键：和vim的常用快捷键差不多

```shell
  进入命令行模式:
    ESC          | 进入命令行模式

  进入输入模式:
    i            | 在光标前插入
    a            | 光标后插入
    I            | 在行的开头插入
    A            | 在行的结尾插入
    c<mov. comm> | Change text of a movement command <mov. comm> (见下文).
    C            | 剪切到行尾 (同 c$)
    cc 或 S      | 剪切整行 (同 0c$)
    s            | 删除光标处文本，并进入插入模式。 (同 c[SPACE])
    r            | 修改光标处文本 (没有离开命令样式)
    R            | 进入替换模式
    v            | 先执行命令，再使用编辑编辑命令。使用 $VISUAL 或 $EDITOR 变量定义编辑器, 编辑器默认 vi 。

  移动 (命令模式下):
    h            | 按字左移
    l            | 按字右移
    w            | 按词右移
    b            | 按词左移
    W            | 以空白字符按词右移(比如 ab a-b ， W 不会移动到 - 上，而 w 会)
    B            | 以空白字符按词左移
    e            | 移动光标到词尾部
    E            | 以空白符移动光标到词尾
    0            | 移动光标到行首
    ^            | 移动光标到行首不是空白符
    $            | 移动光标到行尾
    %            | 移动到左括号或右括号

  字符查找 (也是移动命令):
    fc           | 右移到字符 c .
    Fc           | 左移到字符 c .
    tc           | 右移到字符 c 的左边
    Tc           | 左移到字符 c 的右边
    ;            | 重做查找
    ,            | 反方向重做查找
    |            | 移到第 n 列 (如 3| 移到第 3 列)

  删除命令:
    x            | 删除当前光标所在字符.
    X            | 删除光标前的一个字符.
    d<mov. comm> | Delete text of a movement command <mov. comm> (see above).
    D            | 删除到行尾 (同 d$).
    dd           | 删除行 (同 0d$).
    CTRL-w       | 向左删除单词 (编辑模式下)
    CTRL-u       | 删除到进入编辑模式时光标位置

  撤销、重做、复制、粘贴:
    u            | 单步撤销
    U            | 撤销所有
    .            | 重做
    y<mov. comm> | Yank a movement into buffer (copy).
    yy           | Yank the whole line.
    p            | 在光标处粘贴
    P            | 在光标前粘贴

  历史记录:
    k            | 上一条命令
    j            | 下一条命令
    G            | 回来当前命令
    /string 或 CTRL-r  | 搜索历史命令(/string 用于命令模式下， ctrl-r 用于输入模式下)
    ?string 或 CTRL-s  | 搜索历史命令(Note that on most machines Ctrl-s STOPS the terminal | output, change it with `stty' (Ctrl-q to resume)).
    n            | 下一条历史匹配
    N            | 上一条历史匹配

  自动完成:
    TAB 或 = 或  | 列出所有可能(TAB 用于输入模式)
    CTRL-i       |
    *            | Insert all possible completions.

  其他:
    ~            | 切换当前光标处文本的大小写，并右移光标
    #            | 注释当前命令并把其放入历史
    _            | Inserts the n-th word of the previous command in the current line.
    0, 1, 2, ... | Sets the numeric argument.
    CTRL-v       | Insert a character literally (quoted insert).
    CTRL-r       | Transpose (exchange) two characters.
```
