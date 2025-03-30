# tmux_tutorial
Step-by-step Tutorial for Tmux

以下是一个完整的 `tmux` 工作流代码，包括新建任务、挂起任务、恢复任务以及关闭任务的操作。通过这些步骤，你可以高效地管理任务和进程。

---

### **1. 新建任务**
使用 `tmux` 创建一个新的会话，并在其中运行任务：

```bash
# 创建一个新的 tmux 会话并命名为 "my_session"
tmux new-session -s my_session -d

# 在会话 "my_session" 中运行一个任务（比如运行 Python 脚本）
tmux send-keys -t my_session "python my_script.py" C-m

# 进入会话查看任务
tmux attach -t my_session
```

---

### **2. 挂起任务**
如果你想挂起任务并返回到普通终端，你有以下两种方式：

#### 2.1. 挂起整个会话：
按下快捷键 **`Ctrl+b`**，然后按 **`d`**，会将整个 `tmux` 会话挂起到后台。你会看到类似如下提示：
```
[detached from session my_session]
```

会话被挂起后，你可以在终端中继续其他操作。

#### 2.2. 挂起单个任务：
如果你只想挂起某个特定任务，可以通过以下方式：
```bash
# 挂起任务（使用 shell 的 Ctrl+Z 快捷键）
Ctrl+Z
# 然后将任务放入后台运行
bg
```

---

### **3. 恢复任务**
你可以从挂起状态恢复任务。

#### 3.1. 恢复整个 `tmux` 会话：
列出所有挂起的 tmux 会话：
```bash
tmux list-sessions
```

输出类似：
```
my_session: 1 windows (created Mon Mar 30 12:00:00 2025) [80x24]
```

重新连接到会话：
```bash
tmux attach -t my_session
```

#### 3.2. 恢复单个挂起任务：
如果使用 **`Ctrl+Z`** 挂起了任务，可以通过以下方式恢复：

- 列出挂起的任务：
  ```bash
  jobs
  ```
  输出类似：
  ```
  [1]+  Stopped    python my_script.py
  ```

- 将任务恢复到前台：
  ```bash
  fg %1
  ```
  或让任务在后台运行：
  ```bash
  bg %1
  ```

---

### **4. 关闭任务**
关闭任务可以通过以下几种方式完成：

#### 4.1. 关闭进程：
直接在 `tmux` 面板中终止任务：
```bash
Ctrl+C
```

#### 4.2. 关闭整个 `tmux` 会话：
如果你确认不需要再使用会话，可以关闭整个 `tmux` 会话：
```bash
tmux kill-session -t my_session
```

#### 4.3. 查找并关闭进程：
如果你想手动查找并关闭某个任务的进程，可以这样操作：

- 找到任务的 PID：
  ```bash
  ps aux | grep my_script.py
  ```

- 杀掉任务的进程：
  ```bash
  kill -9 <PID>
  ```

---

### **完整代码示例**
下面是一个完整的流程代码，从新建任务到关闭任务：

```bash
# 1. 新建一个 tmux 会话并运行任务
tmux new-session -s my_session -d
tmux send-keys -t my_session "python my_script.py" C-m

# 2. 挂起会话
tmux detach -t my_session

# 3. 恢复会话
tmux attach -t my_session

# 4. 关闭会话
tmux kill-session -t my_session
```

---

### **快捷操作总结**
- **新建会话**：`tmux new-session -s <session_name>`
- **挂起会话**：`Ctrl+b` 然后按 `d`
- **恢复会话**：`tmux attach -t <session_name>`
- **关闭会话**：`tmux kill-session -t <session_name>`
