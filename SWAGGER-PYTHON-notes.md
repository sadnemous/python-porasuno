# python-porasuno
### Create venv
```bash
mkdir venv
sudo apt install python3.12-venv
python3 -m venv $PWD/venv
. venv/bin/activate
pip install flask
pip install uvicorn
pip install flasgger
pip install flask-restful
vim swagg.py
```
### Add this to swagg.py
```python
#!venv/bin/python3
from flask import Flask
from flask_restful import Resource, Api
from flasgger import Swagger

app = Flask(__name__)
api = Api(app)
swagger = Swagger(app)


class Books(Resource):
    def get(self):
        '''
        Get a list of books.

        ---
        responses:
          200:
            description: A list of books.
            schema:
              type: array
              items:
                type: object
                properties:
                  title:
                    type: string
                  author:
                    type: string
        '''
        books = [
            {'title': 'Book 1', 'author': 'Author 1'},
            {'title': 'Book 2', 'author': 'Author 2'},
        ]
        return books


api.add_resource(Books, '/books')

if __name__ == '__main__':
    app.run(debug=True)
```

### Run the python script
```bash
chmod +x swagg.py
./swagg.py
```

#### Open browser, and access Swagger UI at http://localhost:5000/apidocs. Explore..<br>


####Source: https://www.geeksforgeeks.org/swagger-ui/
