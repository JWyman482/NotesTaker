# NotesTaker
AWS-enabled note taking application. Front-end is a Vue.JS application using Vuetify with a RESTful API call to AWS API Gateway, which then calls a Lambda function. The Lambda function controls actions in an AWS RDS MySQL database.

## Front-End
[Vue.JS](https://vuejs.org/) with [Vuetify](https://vuetifyjs.com/en/) is used for the front-end. The site materials are hosted in an S3 bucket. The site uses an async fetch request to call API Gateway, which then activates a lambda that updates the database at Amazon RDS.


## API

### Requests
Interactions with the DB are controlled by the "action" property on the request. Additional properties change based on the action, but are typically "name", "id" and "item_id". Example:
```javascript
{
  "action": "get",
  "id": "id",
  "item_id": "1234"
}

```

##### Action == Get.
Default: Returns all entries in the DB.
Additional Properties: If the request includes "id": "id" and "item_id": "####" where the # is a four-digit id number, the request will only return a single object.
##### Action == Insert.
Requires "name": "xxxxx" where 'x' is a string to be included. A new entry will be added with a serialized ID.
##### Action == Delete.
Default: Requires "item_id": "####" where # is the serialized id of the entry to delete.
##### Action == Update.
Default: Requires "item_id": "####", "name": "xxxxxxx" where # is the id of the entry to update, and 'x' is the updated entry.

### Response
```javascript
{
"item_id": "####",
"name": "xxxxxxx"
}
```
