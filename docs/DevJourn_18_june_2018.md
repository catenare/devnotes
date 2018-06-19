# Developer Journal Week of 18 June 2018
Goal this week is to at least finish the admin part of *lookfindme*. So close but for the details.

## Monday, 18 June 2018
Still working on lookfindme admin site. Having issues with the industries list. Not updating if there is only one item in the json array. Don't know why that it is. It will save okay but it seems to have an issue updating. Will check the interwebs else might just convert it to an array or a string with pipe characters and store it as a string. The data is actually being sent. The issue is the it is not being saved.
* Using integers for all my money. Listened to a webcast about using integers for currency rather than floats. Requires a little more on the front-end side but then, I'm trying to avoid anything on the front-end that will have to be redone on the backend anyway. 
* 
### lookfindme
* Look into why the industries list of positions doesn't want to update if there is only 1 item in the list.
	* Resolved by adding *synchronize_session='evaluate'* - `            result = self.query.filter(self._table.uuid == uuid).update(update_values, synchronize_session='evaluate')` [Query Details](http://docs.sqlalchemy.org/en/latest/orm/query.html?highlight=query)
* Now have to work on the enable/disable issues.
	* Fix the issue with the database not respecting UUIDs passed in from the API. Only seems to be an issue when I'm not passing it in as a primary key. No problem if it is a primary key. [SQLAlchemy Schema Table](http://docs.sqlalchemy.org/en/latest/core/metadata.html#sqlalchemy.schema.Table) - [Postgresql.UUID](http://docs.sqlalchemy.org/en/latest/dialects/postgresql.html?highlight=uuid#sqlalchemy.dialects.postgresql.UUID)

**database/engine.py**
```python
class SiteSettings(base):
    __table__ = Table(
        c.TABLE_SITE,
        meta,
        Column('site_uuid', postgresql.UUID(as_uuid=True)),
        autoload=True,
        autoload_with=engine,
        extend_existing=True
    )
```
**routes/admin.py**
```python
@bp.route('/site/<uuid:site_id>', methods=['GET'])
def site_get(site_id):
    try:
        result = SiteServiceModel.get_json_data(site_id)
    except SQLAlchemyError as err:
        response = SiteServiceModel.get_response_error(err)
    else:
        response = SiteServiceModel.get_response_result(result)
    return response
```
* It is **elif** in python. 
* Remove dictionary key - `record_data.pop('uuid', None)` Does not raise an error but returns *None* as default.
* Had to update my tests. Apparently, unless you spell out the complete test, it is not being run. But the tests are at least  running now.
* Finally got the industry list to work correctly. Now can update and enable them. On the industry, we allow editing an industry if it is not enabled. Once enabled, it can't be edited. Don't really check for that in the backend. Should put in a check for that. But I'm done with the industry list for now. Going to work on the settings part. Trying to make the settings part into tabs. Seems like a better idea than the drop down. Also need to change what we are storing in the settings object. Don't think we need images anymore. Another question is, do we break things up into their own columns? Since we are saving the complete record every time, don't think we need to.
* Tabs look okay. Not going to win any awards for the layout or design. Need to see which css framework will work okay with vuetify. Adding a new item to the top of a JavaScript array - `unshift`. Assume it plays hell on the memory but it looks better.
* Updated create scripts for database. Now need to work on authentication and security to make sure that works okay.
* Going to work on authguard and aws amplify again. What do I need to notify when things change?
* Going to attempt to get the current session and get the necessary token to auth with our api gateway service. Still not really clear which service is best for this.
* `(await Auth.currentSession()).idToken.jwtToken` - Getting the cognito jwtToken for authorisation with the API gateway.
* Instructions for updating api server
	* Pull in changes `git pull origin master`
	* stop uwsgi - `uwsgi --stop /tmp/lookfindme.pid`
	* Update database - *tools/database* `gradle migrate`
	* start uwsgi - `uwsgi --ini uwsgi.ini --plugin python3`
	* restart nginx - `sudo /etc/init.d/nginx restart`
* Major rxjs magic to include a call to the auth server before calling our api gateway server.
```typescript
  return GetCurrentSession$().pipe(
    switchMap( (data) => ajax(
      {
        method: reqMethod,
        url: reqUrl,
        body: reqBody,
        headers: Object.assign({}, {'Content-Type': 'application/json', 'Authorization': data.idToken.jwtToken}, reqHeaders)
      }
    ).pipe(
      tap ( data => logger.debug('ajax response', data)),
      map (data => data.response.result))
    )
```
Going to build it and see if it works.