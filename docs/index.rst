Flask-Mongobit |release| documentation
===========================================

.. module:: flaskext.mongobit

Overview
---------
**Flask-Mongobit** is a simple wrapper for `Mongobit`_.

Installation
------------------------

Install the extension with one of the following commands:::

  $ easy_install flask-mongobit

or alternatively if you have pip installed::

  $ pip install flask-mongobit

Configuration
------------------

**DB_HOST**: default is **localhost**

**DB_PORT**: default is **27017**

**DB_NAME**: database name

**DB_AUTH**: need auth or not, default is **False**

**DB_USER**: needed if **DB_AUTH** is **True**

**DB_PASS**: needed if **DB_AUTH** is **True**

How to use
------------
In your Flask app file (e.g. myapp.py)::

    from flask import Flask
    from flask_mongobit import MongoBit

    app = Flask("myapp")
    db = MongoBit(app)
    # or
    # db = MongoBit()
    # db.init_app(app)

    # in your models file (e.g. models.py)
    from myapp import db

    class User(db.model):
        coll_name = "users"
        # will add created_at and updated_at automatically if set True
        # and will update updated_at if update doc
        use_ts = True
        username = db.str(unique=True)
        display_name = db.str(index=True)
        logged_in = db.bool(index=True, default=False)

    # then in your views py (e.g. views.py)
    from flask import render_template
    from myapp import app
    from models import User

    @app.route("/")
    def index():
        spec = {}
        # fill spec if needed
        users = User.find(spec=spec)
        return render_template("users.html", users=user)

Deep into the Mongobit
--------------------------

Below are supported field types (used for value type checking).

    **str**: str

    **unicode**: six.text_type

    **bool**: boolean type

    **list**: list type

    **dict**: dict type

    **int**: integer type

    **float**: float type

    **tuple**: tuple

    **date**: date

    **datetime**: datetime

    **objectid**: ObjectId type

    **any**: not check value type

API
------------------

**see source code**

.. autoclass:: FlaskMongobit
   :members:

.. toctree::
   :maxdepth: 2

.. _Flask: http://flask.pocoo.org/
.. _pymongo: http://pypi.python.org/pypi/pymongo/
.. _mongobit: https://github.com/lixxu/mongobit
