# lab3
                flask и Бд
        service_db=# SELECT * FROM service.users;
         id |         full_name         |  login   | password
        ----+---------------------------+----------+----------
          1 | <Полное имя пользователя> | <логин>  | <пароль>
          2 | <Ivanov Ivan>             | <Ivanov> | <123456>
          3 | a                         | first    | a1234
          4 | b                         | two      | b1234
          5 | c                         | three    | c1234
          6 | d                         | four     | d1234
          7 | f                         | five     | f1234
          8 | g                         | six      | g1234
          9 | h                         | seven    | h1234
         10 | j                         | eight    | j1234

ACCOUNT

        <!DOCTYPE html>
                <html lang="en">
        <head>
            <meta charset="UTF-8">
            <title>Title</title>
            <form action="" method="post">
                {% if full_name %}
                <p>Hello, {{full_name}}! </p>
                {% endif %}
        
        	</p>
        
                    </form>
        </head>
        <body>
        
        </body>
        </html>
        
LOGIN

       <!DOCTYPE html>
       <html lang="en">
       <head>
    <meta charset="UTF-8">
    <title>Login</title>
       </head>
       <body>
    <form action="" method="post">
        <p>
     <label for="username">Username</label>
     <input type="text" name="username">
        </p>
        <p>
     <label for="password">Password</label>
     <input type="password" name="password">
        </p>
        <p>
     <input type="submit">
        </p>

        </form>

       </body>
       </html>
       
       
MAIN

      import requests
      from flask import Flask, render_template, request, redirect
      import psycopg2
      
      app = Flask(__name__)

      conn = psycopg2.connect(database="service_db",
                        user="postgres",
                        password="1234",
                        host="localhost",
                        port="5432")
      cursor = conn.cursor()

      @app.route('/login/', methods=['GET'])
      def index():
         return render_template('login.html')
   
         @app.route('/login/', methods=['POST'])
      def login():
          username = request.form.get('username')
          password = request.form.get('password')
          cursor.execute("SELECT * FROM service.users WHERE login=%s AND password=%s", (str(username), str(password)))
          records = list(cursor.fetchall())

    return render_template('account.html', full_name=records[0][1])
