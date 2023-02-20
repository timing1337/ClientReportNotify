# ClientReportNotify

Decode:
```
function decodeClientReportNotify(buf){
    const clonedBuf = Buffer.from(buf);
    let i = clonedBuf.length;
    while (i >= 0) {
        if (i == clonedBuf.length - 1) {
            clonedBuf[i] = clonedBuf[i] ^ 0xA3
        } else {
            clonedBuf[i] = clonedBuf[i] ^ clonedBuf[i + 1]
        }
        i--;
    }
    return clonedBuf.toString('utf-8');
}
```

```
Sample: 591313186179111d1d1d1e127f710e12121861686e20de
Result: {"1":["3.3.0"],"0":[3]}
```

Encode
```
function encodeClientReportNotify(report){
    const buf = Buffer.from(report, 'utf-8');
    for(let i = 0; i < buf.length; i++){
        if(i == buf.length - 1){
            buf[i] = buf[i] ^ 0xA3
        }else{
            buf[i] = buf[i] ^ buf[i + 1]
        }
    }
    return buf;
}
```

```
Sample: {"1":["3.3.0"],"0":[3]}
Result: 591313186179111d1d1d1e127f710e12121861686e20de
```
