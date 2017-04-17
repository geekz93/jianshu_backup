使用windows的工具，netsh进行修改
```
import sys   
import os   

def setDns(config):  
    '''''config = (name,dns)'''  
    if config[1]:  
        cmd = 'netsh interface ip set dns name=%s source=static %s primary' % config  
    else:  
        cmd = 'netsh interface ip set dns name=%s source=dhcp' % config[0]  
  
    os.system(cmd)  
  
def setIp(config):  
    '''''config = (name,ip,mark,gateway)'''  
    if config[1]:  
        cmd = 'netsh interface ip set address name=%s source=static %s %s %s 1' % config  
    else:  
        cmd = 'netsh interface ip set dns name=%s source=dhcp' % config[0]  
  
    os.system(cmd)  
  
def setConfig(config):  
    setIp(config[0:4]);  
    setDns((config[0], config[4]))  
      
def loadConfig(filename):  
    with open(filename) as f:  
        name = "无线网络连接"  
        ip = f.readline().strip()  
        mark = f.readline().strip()  
        gateway = f.readline().strip()  
        dns = f.readline().strip()  
        return (name, ip, mark, gateway, dns)  
      
if __name__ == "__main__":  
    if len(sys.argv) > 1:  
        ipConfig = loadConfig(sys.argv[1])   
    else:  
        ipConfig = ["无线网络连接", "10.24.42.132", "255.255.192.0", "10.24.0.1", "202.204.60.10"]#, "202.204.48.8"
    num = input("ip number:")
    ip = '10.24.42.'+num
    ipConfig[1] = ip
    setConfig(tuple(ipConfig))
    print('IP修改为: %s'%ip)
    os.system("pause")
```
