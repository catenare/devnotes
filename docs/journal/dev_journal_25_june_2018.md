# Week of 25 June 2018
## Monday 25 June 2018
* Decided to bypass on meetup. Need to finish up with KinderCare login issue. Want to work on lookfindme tomorrow.
* KinderCare
    * Icon for home
    * Spent too much time worrying about the toolbar.
    * Notes
        * Will have a different layout for each section.
        * Can even have different colour schemes.
        * Still trying to get my head around Covalent
            * []() 
            * [Flex Layout](https://github.com/angular/flex-layout/wiki/Fast-Starts)
            * [*docs](https://teradata.github.io/covalent/#/docs)
    * Logging in - checking if logged in
        * Observable returned from verifySession. Returns an error if not logged in.
        * This seems to catch the error and then run the redirect for the error.
        * If there is no error, should return the boolean true.

```typescript
  checkLoginUrl(url: string): Observable<boolean> {
    console.log('check login url: ', url);
    return this.authService.verifySession().pipe(
      tap( data => console.log(data)),
      switchMap( data => of(true)),
      catchError( err => {
        console.log('error', err);
        this.router.navigate(['/auth/login']);
        return of(false);
      }
      ),
    );
```

* Reactive Forms
    * Be sure to import the *ReactiveFormsModule*.
* Got authentication working on the site. Can login with email address and password. Seems like they fixed that issue with email address as password.
* When updating a password, need to send in the whole user object and then add the challengeParams separately.


```js
  newPasswordSubmit() {
    const newPassword = this.newPasswordForm.value.newPassword;
    this.authService.completeNewPassword(
      this.authUser, newPassword
    ).subscribe(
      data => this.processLogin(),
      err => logger.error('new password error', err)
    );
  }

  completeNewPassword(user, password) {
    return from(Auth.completeNewPassword(user, password, user.challengeParam.requiredAttributes)).pipe(
      catchError(
        err => throwError(err)
      )
    );
  }
```

* Need create siteId for all new users. Need to create an admin screen for setting up new users. Create with cognito.
* Error message when showing my data. Going to create a resolver to pull the data before we go to that url.
* Added a dashboard module.
* Redoing class (models) to better manage my data.
    * Make it easier with registration.
## Tuesday 26 June 2018
* Not getting things done. Really frustrating.
    * @KevlinHenney
    * Redoing list of accounts
* Things are not flowing today. It's a big issue. Have to get this done because I need to get some income in the next few weeks.
* Resolvers in Angular (getting the children back from the database). Can have it automatically fetch data based on the URL. - [Route Resolvers](https://alligator.io/angular/route-resolvers/)
* [Property Practitioner's Bill](http://ewn.co.za/2018/06/26/property-practitioners-bill-gains-momentum) - store data for 10 years.
    * Regulate real estate agency.
* Redoing the tables now that I have a better idea of how they work. Can make them much cleaner now.
* Bug in *mat-header-row*. Had to upgrade to the latest version.
* Was able to setup.
    * Filtering
    * Sorting
    * Sticky headers and footers
    * Get data from the database.
* Working on the directory service. Get all the people or parents.
    * Hopefully get the service to work.
## Wednesday 27 June 2018
* Did not get much done yesterday. Need to get the registration done so I can move on.
* Tasks
- [x] Setup logging service for Python
    - [x] Insight into API services.
    * [Python Logging API](https://docs.python.org/3/library/logging.html)
        * *Logger* class
        * Keyword args - exception info, stack info = stack frames unwound including calling the logger, extra = dict with your message details.
        * *logging.debug(msg, \*args, \*kwargs)*
    * Basic logging
        * `import logging`
        * `logging.info("message")`
        * *warning* is the default level. Need to have warning or better to see what is going on.
    * Basic logging works. Can now see what is going on in my API. Makes it easier to troubleshoot. Going for a run now.
    * All tests are now working. Made a change that caused tests to break. Tried to fix the tests rather than fixing the issues that caused the test to break.
- [ ] Test service for POST to python service
    * Fixing tests before redoing registration service
        * Adding random to year and month for testing monthend
        * Want to insure all tests work before pulling registration apart.
        * Trying to upgrade marshmallow dependency to the latest. Pipenv really slow.
        * Running tests to see if this code still works.
        * Tests are now working with latest version of Marshmallow.
        * JsonSchema and marshmallow_schema does not work with Marshmallow 3
    - [ ] Post data to service
    - [ ] Create invoice for service
        - [ ] Line Items
            - [ ] Registration
            - [ ] Toiletries
            - [ ] School fees
            - [ ] Discounts
- [ ] Test angular service.

* Everything is running so slow!!!!
* Got the logging to work.
* Cleaned up test url
* Feel like I'm literally running out of time.
* Uncle Bob
    * A good architecture maximises the decision you don't have to make.
        * plugin model
    * Framework author have their interest in mind, not yours. You have a tremendous commitment to the framework, they have no commitment to you.
* Just came back after a talk on AI. Was interesting talking to the folks there.
## Thursday 28 June 2018
* Seems like I can't get anything done. Need to redo the registration module. Maybe do need to break it into modules. Already have done that since every piece has it's own service. Focus on getting the 3 things done, lookfindme, kindercare, headless wordpress in fargate (wordpress as a 12 ? app).
* Trying to get json test string to work in Python
* With marshmallow, keep forgetting that it is already getting json data. Need to convert data to json first before feeding 
* **marshmallow needs json** - stick that into your head.
* I feel like I keep forgetting this stuff. Anyway, need to pass in integers for fees. Going to convert all my currency data to integers to avoid dealing with floating errors.
* Show log warnings. Have to configure in pytest.ini - [Live Logs in PyTest](https://docs.pytest.org/en/latest/logging.html#live-logs)

```ini
[pytest]
addopts = --capture=no --maxfail=2
log_cli=true
```

* Trying to see if there is a way to run multiple individual tests from the command line.
* Cool. All tests still pass.

[SpeakerDeck Raymond Hettinger](https://speakerdeck.com/pyconslides/transforming-code-into-beautiful-idiomatic-python-by-raymond-hettinger-1?slide=13)

```python
names = ['raymond', 'rachel', 'matthew']
colors = ['red', 'green', 'blue', 'yellow']
for color in reversed(colors):
    print(color)

for i, color in enumerate(colors):
    print(i, color)
    
for name, color in izip(names, colors):
    print(name, '--->', color)

for color in sorted(colors, reverse=True):
    print(color)

for color in sorted(colors, key=len):
    print(color)
    
for i, value in enumerate(seq):
    if value == tgt:
        break
    else: # if not found
        return -1
    return i

for k,v in d.iteritems():
    print(k,v)
    
# count items in a dictionary
colors = ['red', 'green', 'red', 'blue', 'green', 'red']
d = {} 
for color in colors:
    if color not in d:
        d[color]=0
    d[color] += 1
    
# with get
colors = ['red', 'green', 'red', 'blue', 'green', 'red']
d= {}
for color in colors:
    d[color] = d.get(color, 0) + 1 # for the lookup to not fail

d = defaultdict(int)
for color in colors:
    d[color] += 1

d = {} #grouping
for name in names:
    key = len(name)
    if key not in d:
        d[key] = []
    d[key].append(name)

d = {}
for name in names:
    key = len(name)
    d.setdefault(key, []).append(name)

d = defaultdict(list)
for name in names:
    key = len(name)
    d[key].append(name)
    
twitter_search('@obama', False, 20, True)
twitter_search('@obama', retweets=False, numtweets=20, popular=True)
```

* Create an object dictionary from a dictionary - [Python Dict Object](https://goodcode.io/articles/python-dict-object/)

```python
class objectview(object):
    def __init__(self, d):
        self.__dict__ = d
        
d = {'a': 1, 'b': 2}
o = objectview(d)
assert o.a == 1
assert o.b == 2
d['c'] = 3
assert o.c == 3
del o.c
assert 'c' not in d
```

PythonTutor - step through your code - [Python Tutor](pythontutor.com)

* Something that is supposed to be straightforward is not working. I don't know why. Finally got it to work. Related to the data for the test. Tests need to represent what I'm working on.
* Going to try and insert data with ORM
* Updated my database configuration to allow automatic adding of registration without having to explicitly add it.
```python
child = Child(center_uuid="8e993f1f-a622-4f86-aed6-ac4eb06debbf", first="marcia", last="adams", date_of_birth="2013-05-18", gender="Female",govt_id="1305180835126", account_uuid="52837e8a-ce2c-4c48-93c4-30fb9e269fd6")
session.add(child)
registration = Registration(child=child, center_uuid="8e993f1f-a622-4f86-aed6-ac4eb06debbf", registration_date="2018-06-10", start_date="2018-07-01", class_id=1, is_sibling=False, is_church_member=False, is_new=True, school_year="2018-01-01")
child.registration = registration
session.add(registration)
session.commit()
```

* Python multiprocessing/async - PyBay Keynote [Raymond Hettinger PyBay Keynote](https://www.instapaper.com/hello2?u=https%3A%2F%2Fpybay.com%2Fsite_media%2Fslides%2Fraymond2017-keynote%2Findex.html&t=Raymond%20Hettinger%20Keynote%20%E2%80%94%20PyBay%202017%20Keynote%20documentation&s=&cookie_notice=1)

## Friday 29 June 2018
* Okay. Got the children to actually work. Had to mess with pytest.fixtures because had it as session scope before. Needed function scope to avoid duplicate key violations.
* Fixtures make testing liveable
* Not writing as much today but also feel like I'm finally getting some stuff done.
* Got the child/registration to work. Need to verify that all data is being captured. Guardian seems to be working too. Need to get the person(s) to work and the basic registration should be done. Then have to do the line items and the receipt information.
* Think I'm going to create a workflow in line items for new registrations. Specifics necessary is class, discounts, child_uuid, and account_uuid. Registration is dependent on if the child is_sibling. Class fees is based on additional rules for preschoolers.
* Wonder if we should calculate the total fees for a child based on start date. (?)
* Tests and the single developer. Why they are important.
    * Learn something new
    * Refactoring
    * Upgrading
* Do the initial client setup
    * registration
    * toiletries
    * CQRS - Command query responsibility segregation
* Nap time.
## Saturday 30 June 2018
* Working on finishing the registration. Have the centre results.
* Don't try to make it himself.
    * [JSON Generator](https://next.json-generator.com/VJ-kVrlfH)
* Python is intense. Just spent an hour trying to figure out why something is not working. **I had a comma behind a statement**
* Marshmallow being used with Flask to validate json data before getting or putting into Postgres database.
* Refactored some code. Focusing on making functions only do one of two possible things. Return a value or do a side affect. Make sure to pass in parameters rather than grabbing parameters from the environment, around the object.
* Added marshmallow schema for my settings json object. Able to retrieve them as objects. Using marshmallow schema to change the data around directly without having to do much.
* Focus on keeping app layers separate.
    * service layer - logic/business objects for application. Avoid direct database or table manipulation.
    * model layer - communicate between service and database. Create the object that is sent or retrieved from backend database. 
    * Use marshmallow to maintain some validation with database schema. Use marshmallow to try and at least have a schema for the json fields.
    * `  items = [result for result in center.settings.fees if result.name == search]` - Get item in a list in python by searching for it
* Got the registration and toiletries fees to work. Think I'm just going to grab the school fees from the child view table.
* Took a little bit to figure out where to capture my exception. Need access to the session so I can rollback if necessary.
* asyncio - trying to figure it out.
* Need to do the bank account upload. Then can focus on the front-end. Will also upload the actual code to the server. Can access it from there. Need to get the front-end out.
## Sunday 30 June 2018
* Look into replenishing my Apple account.
* Do the bank statement upload
* Move potentially sensitive data to my OneDrive folder - add link to folder - `ln -s ~/OneDrive/Johan/project\ data/kindercare/data ./data`
* Not making a lot of notes. Working on the banking upload. Code was pretty decent that I wrote. Able to work with multiple files at the same time.
* Testing this process
    * Move file to tmp directory
    * Have account information stored in details
        * Check for account information in details
* Need an article about marshmallow and validating json post data. Also for converting your database objects to json. SQLAlchemy makes it relatively easy to create multiple hierarchy objects to send to the front-end.
* Flask, Marshmallow and SQLAlchemy - api backend.
* Tulip - async/io
* Have to use a regex to find the account details inside a description string so I can process the details for the string.
* Okay. Add the account_uuid to the row but don't process it. Will show up when processing the items.
* Can import banks statements, automatically match the statement with the account and have the statements and receipts update.
* Receipt details now work. Now need to go back to the api again.
* Trying to write tavern tests for statements. For some weird reason, file is not even being recognised.