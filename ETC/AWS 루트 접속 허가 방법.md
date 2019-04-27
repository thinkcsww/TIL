​									**AWS 루트 접속 허가 방법**

------

1. 루트 계정의 비밀번호 설정

   ```
   sudo passwd root
   ```

2. 루트 접속 가능하게 주석 제거 (PermitRootLogin)

3. ```
   sudo vi /etc/ssh/sshd_config
   ```

   3.루트에 .ssh 폴더 생성

4. ```
    sudo mkdir /root/.ssh
   ```

   4. ec2-user의 인증키를 root에 복사

```
sudo cp /home/ec2-user/.ssh/authorized_keys /root/.ssh
```

5. 서버 재시작 

```
sudo service sshd restart
```

