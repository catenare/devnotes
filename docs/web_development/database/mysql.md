# Mysql Notes
* Retrieving data as json
    * [JSON Datatype](https://dev.mysql.com/doc/refman/5.7/en/json.html)
```sql
    select contact_info,
  JSON_EXTRACT(contact_info,'$') as 'extracted',
  JSON_EXTRACT(contact_info, '$.email') as email,
  JSON_EXTRACT(contact_info, '$.message') as message,
  JSON_EXTRACT(contact_info, '$.fullname') as name,
  JSON_EXTRACT(contact_info, '$.telephone') as telephone
from wp_contact_us;
```
