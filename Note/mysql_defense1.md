防数据库被入侵  
====

## 被入侵的数据库  
```Python  
from pymysql import connect

class JX(object):
    def __init__(self):
        # 显示所有商品
        self.conn = connect(host='localhost', port=3306, database='shop',
                       user='root', password='XXXXXX', charset='utf8')
        self.cursor = self.conn.cursor()

    def __del__(self):
        # 收回对象销毁
        self.cursor.close()
        self.conn.close()
        print('结束查询 关闭数据库')

    def exectue_sql(self, sql):
        self.cursor.execute(sql)
        for temp in self.cursor.fetchall():
            print(temp)

    def show_all_items(self):
        sql = 'select * from goods;'
        self.exectue_sql(sql)

    def show_cates(self):
        sql = 'select name from goods_cates;'
        self.exectue_sql(sql)

    def show_brands(self):
        sql = 'select name from goods_brands;'
        self.exectue_sql(sql)

    def add_brands(self): # 增加数据
        item_name = input('输入新商品分类的名称')
        sql = "insert into goods_brands (name) values('{}');".format(str(item_name))
        print(sql)
        self.cursor.execute(sql)
        self.conn.commit()

    def get_info_by_name(self):
        find_name = input('输入要查询商品的名称')
        sql = "select * from goods where name={};".format(str(find_name))
        print(sql)
        print('------->%s<-------'% find_name)
        self.exectue_sql(sql)


                    # 调用静态方法  被装饰的方法被调用时，不会传递类的实例或者类命，
    @staticmethod   #              意味着可以把一个函数放在类里，但是在这个函数里是不能访问类的实例的，
    def print_menu():        #      在函数实现的功能和类实例无关时候会比较有用。
        print('----京西商城------')
        print('输入1查询 商城 ------所有商品------')
        print('输入2查询 商城 ------所有商品分类------')
        print('输入3查询 商城 ------所有品牌分类------')
        print('输入4添加     ------一个商品分类------')
        print('输入5查询     ------商品信息----------')
        print('输入q        ------退 出------')
        return input('请输入功能对应的序号:')

    def run(self):
        while True:
            num = self.print_menu()
            if num == '1':
                # 查询所有商品
                self.show_all_items()

            elif num =='2':
                # 查询所有分类
                self.show_cates()

            elif num =='3':
                # 查询品牌分类
                self.show_brands()

            elif num =='4':
                # 添加一个商品分类
                self.add_brands()

            elif num =='5':
                # 根据名字查询商品
                self.get_info_by_name()

            elif num =='q':
                print('q退出查询 关闭数据库')
                break
            else:
                print('输入有误，请重输入')
            print('--'*20)
            print('--' * 20)
            print('--' * 20)
        pass

def main():
    jd = JX()
    jd.run()

if __name__ == '__main__':
    main()
```



## 参数化  
- sql语句的参数化，可以有效防止sql注入  
- 注意：此处不同于python的字符串格式化，全部使用%s占位  

```Python  
from pymysql import *

def main():

    find_name = input("请输入物品名称：")

    # 创建Connection连接
    conn = connect(host='localhost',port=3306,user='root',password='mysql',database='shops',charset='utf8')
    # 获得Cursor对象
    cs1 = conn.cursor()


    # # 非安全的方式
    # # 输入 " or 1=1 or "   (双引号也要输入)
    # sql = 'select * from goods where name="%s"' % find_name
    # print("""sql===>%s<====""" % sql)
    # # 执行select语句，并返回受影响的行数：查询所有数据
    # count = cs1.execute(sql)

    # 安全的方式
    # 构造参数列表
    params = [find_name]
    # 执行select语句，并返回受影响的行数：查询所有数据
    count = cs1.execute('select * from goods where name=%s', params)
    # 注意：
    # 如果要是有多个参数，需要进行参数化
    # 那么params = [数值1, 数值2....]，此时sql语句中有多个%s即可 

    # 打印受影响的行数
    print(count)
    # 获取查询的结果
    # result = cs1.fetchone()
    result = cs1.fetchall()
    # 打印查询的结果
    print(result)
    # 关闭Cursor对象
    cs1.close()
    # 关闭Connection对象
    conn.close()

if __name__ == '__main__':
    main()

```

## 案例  
### Simple SQL Injection Example  
The first example is very simple.   
It shows, how an attacker can use an SQL Injection vulnerability to go around application security and authenticate as the administrator.  

The following script is pseudocode executed on a web server.  
It is a simple example of authenticating with a username and a password.  
The example database has a table named users with the following columns: username and password.  
```Python
# Define POST variables
uname = request.POST['username']
passwd = request.POST['password']

# SQL query vulnerable to SQLi
sql = “SELECT id FROM users WHERE username=’” + uname + “’ AND password=’” + passwd + “’”

# Execute the SQL statement
database.execute(sql)
```

These input fields are vulnerable to SQL Injection.  
An attacker could use SQL commands in the input in a way that would alter the SQL statement executed by the database server.   
For example, they could use a trick involving a single quote and set the `passwd` field to:  
```Python
password' OR 1=1
```

As a result, the database server runs the following SQL query:  
```Python
SELECT id FROM users WHERE username='username' AND password='password' OR 1=1'  
```

Because of the `OR 1=1` statement, the `WHERE` clause returns the first `id` from the `users` table no matter what the `username` and `password` are. The first user `id` in a database is very often the administrator.   
In this way, the attacker not only bypasses authentication but also gains administrator privileges.   
They can also comment out the rest of the SQL statement to control the execution of the SQL query further:  
```Python
-- MySQL, MSSQL, Oracle, PostgreSQL, SQLite
' OR '1'='1' --
' OR '1'='1' /*
-- MySQL
' OR '1'='1' #
-- Access (using null characters)
' OR '1'='1' %00
' OR '1'='1' %16
```

## How to Prevent an SQL Injection  
The only sure way to prevent SQL Injection attacks is input validation and parametrized queries including prepared statements.   
The application code should never use the input directly. The developer must sanitize all input,   
not only web form inputs such as login forms. They must remove potential malicious code elements such as single quotes.   
It is also a good idea to turn off the visibility of database errors on your production sites.   
Database errors can be used with SQL Injection to gain information about your database.  

If you discover an SQL Injection vulnerability, for example using an Acunetix scan,   
you may be unable to fix it immediately. For example, the vulnerability may be in open source code.   
In such cases, you can use a web application firewall to sanitize your input temporarily.  


