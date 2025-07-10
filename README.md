# ShellTool
### 简易的 Shell 工具，可执行简易的 Shell 命令。支持同步和异步命令的执行；支持 Root 模式和非 Root 模式。
#### 使用方法:

```java
        ShellTool shellTool = ShellTool.builder().isRoot(true).create();
        shellTool = ShellTool.obtain();
        ShellResult shellResult = shellTool.cmd("ls").exec();
        if (shellResult != null) {
            boolean result = shellResult.isSuccess();
        }
        shellTool.cmd("""
            if [[ 1 == 1 ]]; then
                echo hello;
            elif [[ 1 == 2 ]]; then
                echo world;
            fi
            """).exec();
        shellTool.cmd("echo hello").async();
        shellTool.cmd("echo world").async(new IExecListener() {
            @Override
            public void output(@NonNull String command, @NonNull String exitCode, @NonNull String[] outputs) {
                IExecListener.super.output(command, exitCode, outputs);
            }
        });
        shellTool.addExecListener(new IExecListener() {
            @Override
            public void output(@NonNull String command, @NonNull String exitCode, @NonNull String[] outputs) {
                IExecListener.super.output(command, exitCode, outputs);
            }

            @Override
            public void error(@NonNull String command, @NonNull String exitCode, @NonNull String[] errors) {
                IExecListener.super.error(command, exitCode, errors);
            }

            @Override
            public void rootResult(boolean hasRoot, @NonNull String exitCode) {
                IExecListener.super.rootResult(hasRoot, exitCode);
            }

            @Override
            public void brokenPip(@NonNull String reason, @NonNull String[] errors) {
                IExecListener.super.brokenPip(reason, errors);
            }
        });
        shellTool.close();
```
