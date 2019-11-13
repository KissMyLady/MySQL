Python对数据库的基本操作  
====
### 增删改基本操作  
```Python
from pymysql import *

def main():
    # 创建Connection连接
    conn = connect(host='localhost',port=3306,database='shop_data',user='root',password='mysql',charset='utf8')
    # 获得Cursor对象
    cs1 = conn.cursor()
    # 执行insert语句，并返回受影响的行数：添加一条数据
    # 增加
    count = cs1.execute('insert into goods_cates(name) values("硬盘")')
    #打印受影响的行数
    print(count)

    count = cs1.execute('insert into goods_cates(name) values("光盘")')
    print(count)

    # # 更新
    # count = cs1.execute('update goods_cates set name="机械硬盘" where name="硬盘"')
    # # 删除
    # count = cs1.execute('delete from goods_cates where id=6')

    # 提交之前的操作，如果之前已经之执行过多次的execute，那么就都进行提交
    conn.commit()

    # 关闭Cursor对象
    cs1.close()
    # 关闭Connection对象
    conn.close()

if __name__ == '__main__':
    main()
```
说明:  conn.commit()方法是提交，类似于确认。  
如果没有这个，mysql数据库里的key(主键)还是会自动增长，防并发。  
多用户要是并发写入一张表里，并发提交确认，而mysql没有保留id，那么将会产生严重的错误情况，在这种情况下，出现了灵异事件来防止UBG。  


### 查单行数据    
```Python  
from pymysql import *

def main():
    # 创建Connection连接
    conn = connect(host='localhost',port=3306,user='root',password='mysql',database='shop_data',charset='utf8')
    # 获得Cursor对象
    cs1 = conn.cursor()
    # 执行select语句，并返回受影响的行数：查询一条数据
    count = cs1.execute('select id,name from goods where id>=4')
    # 打印受影响的行数
    print("查询到%d条数据:" % count)

    for i in range(count):
        # 获取查询的结果
        result = cs1.fetchone()
        # 打印查询的结果
        print(result)
        # 获取查询的结果

    # 关闭Cursor对象
    cs1.close()
    conn.close()

if __name__ == '__main__':
    main()
```

### 查单多行数据  
```Python  
from pymysql import *

def main():
    # 创建Connection连接
    conn = connect(host='localhost',port=3306,user='root',password='mysql',database='shop_data',charset='utf8')
    # 获得Cursor对象
    cs1 = conn.cursor()
    # 执行select语句，并返回受影响的行数：查询一条数据
    count = cs1.execute('select id,name from goods where id>=4')
    # 打印受影响的行数
    print("查询到%d条数据:" % count)

    # for i in range(count):
    #     # 获取查询的结果
    #     result = cs1.fetchone()
    #     # 打印查询的结果
    #     print(result)
    #     # 获取查询的结果

    result = cs1.fetchall()
    print(result)

    # 关闭Cursor对象
    cs1.close()
    conn.close()

if __name__ == '__main__':
    main()
```

### OOP实现功能封装  
```Python  
from pymysql import connect


class JD(object):
    def __init__(self):
        # 显示所有商品
        self.conn = connect(host='localhost', port=3306, database='jx_shop',
                       user='root', password='XXXXXXX', charset='utf8')
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

                    # 调用静态方法  被装饰的方法被调用时，不会传递类的实例或者类命，
    @staticmethod   #              意味着可以把一个函数放在类里，但是在这个函数里是不能访问类的实例的，
    def print_menu():        #      在函数实现的功能和类实例无关时候会比较有用。
        print('----京西商城------')
        print('输入1查询 商城 ------所有商品------')
        print('输入2查询 商城 ------所有商品分类------')
        print('输入3查询 商城 ------所有品牌分类------')
        print('输入4添加     ------一个商品分类------')
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
    jd = JD()
    jd.run()

if __name__ == '__main__':
    main()

```

