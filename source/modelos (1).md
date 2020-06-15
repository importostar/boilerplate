---
title: modelos (1)
date: 2020-05-07
---
Example Python program modelos (1).py


## Classes

* class Cliente:

## Methods

* def __init__(self, id=None, nome="", telefone="", email=""):
* def save(self, con, tabela=""):
* def load(cls, id, con, tabela=""):
* def last_id(cls, con, tabela=""):
* def cria_tabela(cls, con, tabela=""):
* def campos(cls):
* def __repr__(self):

## Code

Python example

    
    class Cliente:
        tabela = "clientes"
        def __init__(self, id=None, nome="", telefone="", email=""):
            self.id = id
            self.nome = nome
            self.telefone = telefone
            self.email = email
            
        def save(self, con, tabela=""):
            
            if not self.id:
                con.execute("""INSERT INTO {tabela} 
                        ('nome', 'telefone', 'email') 
                        VALUES(?, ?, ?) """.format(tabela=(tabela if tabela else self.tabela)),
                        (self.nome, self.telefone, self.email))
            else:
                con.execute("""
                    UPDATE {tabela} SET
                    nome=?, telefone=?, email=?
                    WHERE id=?
                """.format(tabela=(tabela if tabela else self.tabela)),
                        (self.nome, self.telefone, self.email, self.id))
            con.commit()
    
        @classmethod
        def load(cls, id, con, tabela=""):
            cursor = con.execute("""SELECT id, nome, telefone, email  FROM {tabela} WHERE id=?""".format(tabela=(tabela if tabela else cls.tabela)), (id,))
            dados = cursor.fetchall()[0]
            cliente = Cliente(*dados)
            return cliente
        
        @classmethod
        def last_id(cls, con, tabela=""):
            response = con.execute("""SELECT MAX(id) FROM {tabela}""".format(tabela=(tabela if tabela else cls.tabela))).fetchall()[0][0]
            return response if response is not None else 0
            
            
        @classmethod
        def cria_tabela(cls, con, tabela=""):
            con.execute("""CREATE TABLE IF NOT EXISTS
                {tabela}
                (id integer primary key autoincrement,
                 nome char,
                 telefone char,
                 email char
                )
            """.format(tabela=(tabela if tabela else cls.tabela)))
            
        @classmethod
        def campos(cls):
            return [
            {'name': 'nome', 'label': 'Nome', 'type': str},
            {'name': 'telefone', 'label': 'Telefone', 'type': str},
            {'name': 'email', 'label': 'E-mail', 'type': str},
        ]  
        
        def __repr__(self):
            return "<Cliente '{}', {}, {}>".format(self.nome, self.telefone, self.email)
        
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
