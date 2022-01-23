---
title: sqlalchemy
updated: 2020-09-10 22:07:13Z
created: 2020-09-10 22:07:13Z
---

# SQLAlchemy Notes

## Treat a view as a table in SQLAlchemy and allow use with ORM for queries.
* [Reflect a PostgreSQL view in Python’s SQLAlchemy](https://hultner.github.io/quickbits/2017-10-23-postgresql-reflection-views-python-sqlalchemy.html)
* Ref: [How do I map a table that has no primary key](http://docs.sqlalchemy.org/en/latest/faq/ormconfiguration.html#how-do-i-map-a-table-that-has-no-primary-key)
  * How to reflect views for the ORM
```
engine = create_engine(config('DB_URI'))
meta = MetaData()
meta.reflect(bind=engine, schema='public', views=True)
base = automap_base(metadata=meta)
base.prepare()

def get_table(table_name):
    try:
        result = base.classes[table_name]
    except KeyError as err:
        result = meta.tables[table_name]
    return result

CHILD_VIEW = 'public.child_view'


class ChildView(base):
    __table__ = get_table(CHILD_VIEW)
    __mapper_args__ = {
        'primary_key': [__table__.c.account_uuid]
    }

base.prepare()
```

## [Automap](http://docs.sqlalchemy.org/en/latest/orm/extensions/automap.html)
* Use to automatically get table details from the database. This is if the table is being managed separately from *sqlalchemy*.

## Notes
* Delete with session. [ORM Delete](http://docs.sqlalchemy.org/en/latest/orm/query.html#sqlalchemy.orm.query.Query.delete)
## Examples
* Order By - returns the latest item with the site_uuid.
```python
    return self.query.filter(self._table.site_uuid == uuid).order_by(
      self._table.updated_at.desc()
      ).first()
```