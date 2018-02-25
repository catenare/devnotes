# SQLAlchemy Notes

* [Reflect a PostgreSQL view in Python’s SQLAlchemy](https://hultner.github.io/quickbits/2017-10-23-postgresql-reflection-views-python-sqlalchemy.html)
  * How to reflect views for the ORM
```
class ChildView(db.declarative_base):
    __table__ = db.get_table(CHILD_VIEW)
    __mapper_args__ = {
        'primary_key': [__table__.c.acct_uuid]
    }
```
  * Ref: [How do I map a table that has no primary key](http://docs.sqlalchemy.org/en/latest/faq/ormconfiguration.html#how-do-i-map-a-table-that-has-no-primary-key)

