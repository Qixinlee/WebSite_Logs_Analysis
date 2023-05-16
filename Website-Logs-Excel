# Author Qixinlee
 
import re
import pandas as pd

# 定义日志文件路径
log_file_path = "D:/web/www.qixinlee.com_nginx.log"

# 定义Excel文件路径
excel_file_path = "D:/web/www.qixinlee.com_nginx.xlsx"

# 定义正则表达式来解析日志文件
log_pattern = r'(?P<host>\S+) (?P<identity>\S+) (?P<user>\S+) \[(?P<time>.*?)\] "(?P<request>.*?)" (?P<status>\d+) (?P<size>\S+) "(?P<referrer>.*?)" "(?P<user_agent>.*?)"'

# 打开日志文件并逐行读取内容
log_data = []
with open(log_file_path, "r") as f:
    for line in f:
        match = re.match(log_pattern, line)
        if match:
            request = match.group("request").split()
            log_data.append({
                "访问时间": match.group("time"),
                "访问者IP地址": match.group("host"),
                "请求方式": request[0],
                "请求链接": request[1],
                "请求参数": request[1].split("?")[1] if len(request[1].split("?")) > 1 else "",
                "HTTP协议": request[2],
                "返回状态码": match.group("status"),
                "返回包的长度": match.group("size"),
                "请求包的Referer": match.group("referrer"),
                "访问者的浏览器信息": match.group("user_agent")
            })

# 将结果输出到Excel文件
df = pd.DataFrame(log_data)
df.to_excel(excel_file_path, index=False)
print("结果已输出到Excel文件中：", excel_file_path)
