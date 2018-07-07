# learning 這是我學習經驗中遇到的小問題

## LINUX篇

1.netstat -tunlp (查看端口)   kill -9 PID (強制關閉端口) pkill -kill -t tty2(強制登出）

2.last (查看登入紀錄) lastlog(查看最近一次登入紀錄)

3.ifconfig eth0 192.168.133.150 netmask 255.255.255.0(更改網卡設定)

4.adduser test (root)

  deluser(刪除使用者)  
  
  grep ID /etc/passwd  /etc/shadow /etc/group  
  
  addgroup delgroup gpasswd -a(加入) -d（刪除）帳號　群組

  setfacl -m u:tetst:rwx acl_test1 (acl設定)  
  
  getfacl filename (查看acl設定) 

  chage [-ldEImMW] 帳號名

  選項與參數：
  
  -l ：列出該帳號的詳細密碼參數
  
  -d ：後面接日期，修改 shadow 第三欄位(最近一次更改密碼的日期)，格式 YYYY-MM-DD
  
  -E ：後面接日期，修改 shadow 第八欄位(帳號失效日)，格式 YYYY-MM-DD
  
  -I ：後面接天數，修改 shadow 第七欄位(密碼失效日期)
  
  -m ：後面接天數，修改 shadow 第四欄位(密碼最短保留天數)
  
  -M ：後面接天數，修改 shadow 第五欄位(密碼多久需要進行變更)
  
  -W ：後面接天數，修改 shadow 第六欄位(密碼過期前警告日期)



5.nmap -sS(半TCP) -p 1-65535 -T4(Time) -A(高級) -v
(詳細) -Pn(擋ping) IP

6.passwd (更改密碼)

7.find 【起始目錄】 -name 【欲找的檔名】 -print

8.工具:angry ip 掃網段
http://www.pcnet.idv.tw/pcnet/linux/linux_command.htm

9.monitor :
#!/bin/sh
while [ true ]
do
netstat -anop |grep -v 0.0.0.0 |grep -v unix |grep -v ':::' |grep -v 'Active' |grep -v 'Proto'
echo '****************************************************'
echo ''
echo ''
sleep 0.5
done

10.kill login :
#!/bin/bash 
while [ true ]
do
last | grep -E test | awk {'print $2 '} | while read line
do
    pkill -kill -t  $line
done
echo "***********************"
sleep 0.1
done


11.kill process
#################################
#autoclean.sh
#create for 20180119 CDX contest
#please give me root privileges
#################################
while [ true ]
do
        kill -9  $(netstat -anop  | grep -E "([0-9]{1,3}[\.]){3}[0-9]{1,3}" \
        | awk '{print $5 " " $7}'\  
        |grep -v "0.0.0.0:" \
        |grep -v "127.0.0.1:" \
        |grep -v "10.20.30.11:" \
        |awk '{print $2}' |grep -oE "[0-9]{1,10}/" |grep -oE "[0-9]{1,10}")
        echo '[' $(date) ']:clean'
        sleep 0.1
done


12.ip正規化:
:grep -E "([0-9]{1,3}[\.]){3}[0-9]{1,3}\:[0-9]{0,5}"



13.awk:
http://blog.xuite.net/mb1016.flying/linux/28111008-linux+shell+awk+%E8%AA%9E%E6%B3%95 (過濾字串)
ls -l | awk '{print $1 "   " $2}'

14.echo $()指令 {}字串.數字  c=$[c+1] (數字加法)  echo $[100*966]

15.testfile=/root/Desktop/test.txt
netstat -tuln > ${testfile}  導向記事本

16.“” 雙引號(保持原來屬性) ''單引號(純文字)

17.清除登陸系統成功的記錄，也就是last命令看到的錄 echo >/var/log/wtmp

18.清除登陸系統失敗的記錄，也就是lastb命令看到的記錄echo > /var/log/btmp 

19.清除歷史執行命令 history -c 或者，清空用戶目錄下的這個文件即可 echo > ./.bash_history

20.echo “test” > test.txt  (資料導向）， >>（不覆蓋）

21.正規化: pts.* aa(pts後面到aa所有的字串  )       

[0-9]{1,3}(0-9的數字有1-3個)   

[^a-zA-Z] (不要英文字母)

sed ‘s/要被取代的字串/去取代的字串 /g’ 取代        

grep -v '^\s*$' 刪除空白欄







