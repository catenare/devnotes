# Flask Notes

## Sources
* [Flask](http://flask.pocoo.org)
* [How to Structure Large Flask Applications](https://www.digitalocean.com/community/tutorials/how-to-structure-large-flask-applications)
* [How to serve flask applications with uwsgi and nginx](https://www.digitalocean.com/community/tutorials/how-to-serve-flask-applications-with-uwsgi-and-nginx-on-ubuntu-14-04)

## ~~Creating a Flask App~~ Now using Pipenv
* Create directory and cd into directory
  * `pipenv shell`
* Install flask
  * `pipevn install flask SQLAlchemy psycopg2 click uwsgi`

## Flask with REST API
* Using Marshmallow
    * [Declaring Schemas](https://marshmallow.readthedocs.io/en/latest/quickstart.html#declaring-schemas)
    * Implicit field creation - let marshmallow figure out the field.
```python
class DemoSchema(Schema):
  class Meta:
    fields=("name", "email", "created_at", "uppername")
```

* Using Marshmallow with jsonschema to validate data from api
    * Using marshmallow-jsonschema - [marshmallow-jsonschema](https://github.com/fuhrysteve/marshmallow-jsonschema)
        * Use to dump jsonschema from marshmallow
    * Using jsonschema - [JsonSchema](https://github.com/Julian/jsonschema)
        * Uses jsocshema validate, ValidationError
        * Use the jsonschema from marshmallow-jsonschema to validate content from api
```python
    åsch = ReceiptSchema()
    js_schema = json_schema.dump(sch).data
    receipt = request.get_json()
    try:
        validate(receipt, js_schema)
        receipt_data = sch.load(receipt).data
    except ValidationError as err:
        resp['err'] = err.message
```   
