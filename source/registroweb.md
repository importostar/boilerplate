---
title: registroweb
date: 2020-05-07
---
Example Python program registroweb.py

## Modules

* import datetime
* import sqlite3
* import threading
* from flask import Flask, request, redirect
* # from flask_sqlalchemy import SQLAlchemy
* from jinja2 import Template
* from modelos import Cliente

## Methods

* def get_con():
* def init():
* def hello_world():
* def novo():
* def editar(id):

## Code

Python example

    import datetime
    import sqlite3
    import threading
    
    from flask import Flask, request, redirect
    # from flask_sqlalchemy import SQLAlchemy
    from jinja2 import Template
    
    from modelos import Cliente
    
    app = Flask(__name__)
    
    connections = {}
    
    def get_con():
        thread = threading.current_thread()
        if thread not in connections:
            connections[thread] = sqlite3.connect("../exemplo.db")
        return connections[thread]
    
    def init():
        Cliente.cria_tabela(get_con())
    
    # init()
    
    @app.route("/")
    def hello_world():
        total_clientes = Cliente.last_id(get_con())
        clientes = [Cliente.load(id, get_con()) for id in range(1, total_clientes + 1)]
        template =  Template("""
    <h1>Clientes</h1>
    <a href="novo">Inserir novo cliente</a><br>
    <ul>
    {% for cliente in clientes %}
        <li> 
           <a href="editar/{{ cliente.id }}">
           {{ cliente.nome }}
           </a>, {{ cliente.telefone }}, {{ cliente.email }}
        </li>
    {% endfor %}
    </ul>
    
    """)
        return template.render(clientes=clientes)
    
    
    @app.route("/novo", methods=["GET", "POST"])
    def novo():
        if request.method == "GET":
            template = Template("""
            <h1> Novos dados para {{ nome }}</h1>
            <form action="#" method="POST">
            {% for campo in campos %}
            {{ campo.label }}: <input type="entry" name="{{ campo.name }}"><br>
            {% endfor %}
            <input type="submit" value="Salvar">
            </form>
            """)
            return template.render(campos=Cliente.campos(), nome="Cliente")
        elif request.method == "POST":
            form = request.form
            cliente = Cliente(nome=form["nome"], telefone=form["telefone"], email=form["email"])
            cliente.save(get_con())
            return redirect("/")
            
    @app.route("/editar/<int:id>", methods=["GET", "POST"])
    def editar(id):
        if request.method == "GET":
            cliente = Cliente.load(id, get_con())
            template = Template("""
            <h1> Novos dados para {{ nome }}</h1>
            <form action="#" method="POST">
            <input type="hidden" name="cliente_id" value="{{ dados["id"] }}" >
            {% for campo in campos %}
            {{ campo.label }}: <input type="entry" name="{{ campo.name }}" value="{{ dados[campo.name] }}"><br>
            {% endfor %}
            <input type="submit" value="Salvar">
            </form>
            """)
            return template.render(campos=Cliente.campos(), nome=cliente.nome, dados=cliente.__dict__)
        elif request.method == "POST":
            form = request.form
            cliente = Cliente(nome=form["nome"], telefone=form["telefone"], email=form["email"])
            cliente.id = form["cliente_id"]
            cliente.save(get_con())
            return redirect("/")
            
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
