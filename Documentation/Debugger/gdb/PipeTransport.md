# Pipe Transport
Pipe Transport allows communication through a pipe program to a remote shell. An example on linux would be `ssh`.

## How-To
We have added `"pipeTransport"` as an option within the `launch.json` file. The structure looks as follows:
```
    "pipeTransport": {
        "pipeCwd": "/usr/bin",
        "pipeProgram": "/usr/bin/ssh",
        "pipeArgs": [
            "-pw",
            "<password>",
            "user@10.10.10.10"
        ],
        "debuggerPath": "/usr/bin/gdb"
    },
```
The `pipeArgs` can be any set of arguments necessary to setup and authenticate the pipe connection. In the example, a password is used but you can also use an ssh key.

You may also need to add a `sourceFileMap` to map the path of where the code exists on the remote shell to where it is locally:
```
    "sourceFileMap": {
        // "remote": "local"
        "/home/user/src": "/src/projectA/src"
    }
```

## Attach
You can also use the above `pipeTransport` block to attach to a remote process. In the attach case, you will need to specify a `processId`. We have added the ability to query processes from the remote machine. To do this, change `"processId": "${command.pickProcess}"` to `"processId": "${command.pickRemoteProcess}"`. The `pipeTransport` settings will be used to query the processes on the remote machine. Then select the process from the drop down list. As with `launch`, you may need to configure `sourceFileMap`.  