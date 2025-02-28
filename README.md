# ShellTool
### 简易的 Shell 工具，可执行简易的 Shell 命令.
#### 使用方法:

```java
        ShellTool shellTool = ShellTool.builder().isRoot(true).create();
        shellTool = ShellTool.obtain();
        shellTool.cmd("ls").exec();
        shellTool.cmd("echo hello").async();
        shellTool.cmd("echo world").async(new ShellTool.IExecListener() {
            @Override
            public void output(String command, String[] outputs, String exitCode) {
                ShellTool.IExecListener.super.output(command, outputs, exitCode);
            }
        });
        shellTool.addExecListener(new ShellTool.IExecListener() {
            @Override
            public void output(String command, String[] outputs, String exitCode) {
                ShellTool.IExecListener.super.output(command, outputs, exitCode);
            }

            @Override
            public void error(String command, String[] errors, String exitCode) {
                ShellTool.IExecListener.super.error(command, errors, exitCode);
            }

            @Override
            public void notRoot(String result) {
                ShellTool.IExecListener.super.notRoot(result);
            }

            @Override
            public void brokenPip(String command, String[] errors, String reason) {
                ShellTool.IExecListener.super.brokenPip(command, errors, reason);
            }
        });
        shellTool.close();
```
