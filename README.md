# ShellTool
### 简易的 Shell 工具，可执行简易的 Shell 命令。
#### 使用方法:

```java
        ShellTool shellTool = ShellTool.builder().isRoot(true).create();
        shellTool = ShellTool.obtain();
        ShellTool.ShellResult shellResult = shellTool.cmd("ls").exec();
        boolean result = shellResult.isSuccess();
        shellTool.cmd("""
            if [[ 1 == 1 ]]; then
                echo hello;
            elif [[ 1 == 2 ]]; then
                echo world;
            fi
            """).exec();
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
            public void notRoot(String exitCode) {
                ShellTool.IExecListener.super.notRoot(exitCode);
            }

            @Override
            public void brokenPip(String command, String[] errors, String reason) {
                ShellTool.IExecListener.super.brokenPip(command, errors, reason);
            }
        });
        shellTool.close();
```
