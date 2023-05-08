(label:database)=

# Database

## Getting new databases

We use MongoDB and MinIO to orchestrate the calculations and store the results. Ask Mingjian to create for you a MongoDB on Mongo Atlas and a MinIO bucket hosted at HPE DSI. You will get your MongoDB and MinIO bucket info like:

```yaml
# MongoDB
uri: mongodb+srv://<mongo_username>:<mongo_password>@serverlessinstance0.nisxfj9.mongodb.net/?retryWrites=true&w=majority
database: <database>
username: <mongo_username>
password: <mongo_password>

# MinIO
bucket: <minio_bucket_name>
endpoint_url: http://10.2.1.14:9000
username/access_key_id: <minio_username>
password/secret_access_key: <minio_password>
```

Keep your access info, particularly `<mongo_password>` and `<minio_password>`, confidential.

## Connecting to MongoDB

You can use [Studio3T](https://studio3t.com) to connect to your MongoDB and view your calculations outputs.
