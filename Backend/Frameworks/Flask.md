Install Flask:
``` python
pip install flask
```

Get stated:
```python 
from flask import Flask, render_template, url_for
app = Flask(__name__)
@app.route('/')

def index():
	return render_template('index.html')

if __name__ == "__main__":
  app.run(debug=True)
```

Creating a Database:
```python
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///test.db'

db = SQLAlchemy(app)

class Todo(db.Model):
  id = db.Column(db.Integer, primary_key=True)
  content = db.Column(db.String(200),nullable=False)
  data_created = db.Column(db.DateTime,default = datetime.utcnow)
  
  def __repr__(self):
    return '<Task %r>' %self.id
    
with app.app_context():
  db.create_all()
```
**Note**
The newer version of sqlalchemy requires app.app_context() to be written either in the integrated python shell or within the code itself (just one, comment it out later).

