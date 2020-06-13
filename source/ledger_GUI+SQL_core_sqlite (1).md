---
title: ledger_GUI+SQL_core_sqlite (1)
date: 2020-05-07
---
Example Python program ledger_GUI+SQL_core_sqlite (1).py

## Modules

* from sqlalchemy.ext.declarative import declarative_base
* import sqlite3
* from sqlalchemy import (Column,  # 字段类型
* from sqlalchemy import create_engine
* from sqlalchemy.orm import sessionmaker
* import datetime
* import sqlite3

## Classes

* class 完成的验收名单(ORM基类):  # 定义映射类User，其继承上一步创建的Base
* class 经手现场名单(ORM基类):  # 定义映射类User，其继承上一步创建的Base

## Methods

* def __repr__(self):
* def __repr__(self):
* # def add_one_data(会话, 表):

## Code

Python example

    from sqlalchemy.ext.declarative import declarative_base
    import sqlite3
    ORM基类 = declarative_base()
    from sqlalchemy import (Column,  # 字段类型
                            Integer,  # 下面都是一样的 整型
                            VARCHAR)
    
    
    class 完成的验收名单(ORM基类):  # 定义映射类User，其继承上一步创建的Base
        # 指定本类映射到users表
        __tablename__ = '完成的验收名单'
        # 指定id映射到id字段; id字段为整型，为主键
        ID = Column(Integer, primary_key=True)
        P_ID = Column(VARCHAR(12),unique=True)
        date = Column(VARCHAR(12))
    
        def __repr__(self):
            return f"<b1(ID='{self.ID}', P_ID='{self.P_ID}', date='{self.date}')>"
    
    #
    class 经手现场名单(ORM基类):  # 定义映射类User，其继承上一步创建的Base
        # 指定本类映射到users表
        __tablename__ = '经手现场名单'
        # 指定id映射到id字段; id字段为整型，为主键
        ID = Column(Integer, primary_key=True)
        P_ID = Column(VARCHAR(12))
        date = Column(VARCHAR(12))
        能否安装 = Column(VARCHAR(3))
    
        def __repr__(self):
            return f"<经手现场名单(ID='{self.ID}', P_ID='{self.P_ID}', " \
                f"date='{self.date}',能否安装='{self.能否安装}')>"
    
    from sqlalchemy import create_engine
    engine = create_engine('sqlite:///D:/01_日常规\台账/业务台账.sqlite3')
    # engine是中创建的连接
    from sqlalchemy.orm import sessionmaker
    Session = sessionmaker(bind=engine)
    # 创建Session类实例
    session = Session()
    # session.query(b1).all()
    ORM基类.metadata.create_all(engine)
    
    import datetime
    
    # def add_one_data(会话, 表):
    #     会话.add(表)
    #     会话.commit()
    #     会话.close()
    
    if __name__ == '__main__':
        pass
        import sqlite3
    
        # 现场单 = 经手现场名单(P_ID='DF1900-S001',date="1900-01-02",能否安装='能')
        # # session.add(现场单)
        # session.commit()
        # session.close()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
