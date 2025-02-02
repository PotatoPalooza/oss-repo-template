# Lab 10: Databases
## Checkpoint 0: Project Updates
Discussion and blog update: https://github.com/PotatoPalooza/oss-repo-template/wiki/5.-Week-Three-Progress-Update-Blog

## Checkpoint 1: Install CouchDB
After installing CouchDB on my local machine and visiting `localhost:5984` I get the following result:

![check1](https://user-images.githubusercontent.com/49171429/182263951-66a2539e-7d1c-4520-a92a-02e7321fecd7.PNG)

## Checkpoint 2: Quick Tour

### 1.6.1 All Systems Are Go!
![allsystemsarego](https://user-images.githubusercontent.com/49171429/182265939-5cb97b6c-579f-4465-9394-be91967a8f12.PNG)
### 1.6.2 Welcome to Fauxton
![welcometofauxton](https://user-images.githubusercontent.com/49171429/182266130-adf8dbd1-f4e9-4991-b7ae-a0d783192770.PNG)
### 1.6.3. Your First Database and Document
![dbanddocumentPNG](https://user-images.githubusercontent.com/49171429/182266500-87769daa-dd44-464e-a36b-09ee956fc828.PNG)
### 1.6.4. Running a Mango Query
![runningamangoquery](https://user-images.githubusercontent.com/49171429/182266921-5e520c29-41c1-49e5-825f-079215857b9a.PNG)
### 1.6.5. Triggering Replication
![replication](https://user-images.githubusercontent.com/49171429/182267484-e9514b91-09f3-440a-a72c-94573de6fc74.PNG)

## Checkpoint 3: Now Complete the API Tutorial
### 1.7.1. Server and 1.7.2 Databases
![server](https://user-images.githubusercontent.com/49171429/182268043-40129181-1486-4310-bfe4-92ac277fc77a.PNG)
### 1.7.3. Documents
![1 7 3Documents](https://user-images.githubusercontent.com/49171429/182269486-98dff605-1bdb-4571-ad31-e2c18bfd66f4.PNG)
### 1.7.3.1. Revisions
![1731Documents](https://user-images.githubusercontent.com/49171429/182271200-97589234-b6f3-4436-8200-efdd58bb0cff.PNG)
### 1.7.3.2. Documents in Detail
![1732](https://user-images.githubusercontent.com/49171429/182271410-fda2f372-78ca-473b-a9cd-158961178372.PNG)
### 1.7.3.3. Attachments
I chose an image of a dog to be the artwork.jpg which can be veiwed after the credentials are entered.
![attachments1733](https://user-images.githubusercontent.com/49171429/182272808-d91bf679-4646-47b4-be86-02f0033335c3.PNG)

![attachmentstwoo](https://user-images.githubusercontent.com/49171429/182272924-fef4c54c-935f-4ae8-9c9b-fd0ba4a02222.PNG)
### 1.7.4. Replication
Using the modified command from lab
![dbreplication](https://user-images.githubusercontent.com/49171429/182274090-4ef3fc37-199d-4e3d-b2f5-944497a20bcc.PNG)

![replicationEvidence](https://user-images.githubusercontent.com/49171429/182273987-c6c14042-244f-4b47-983c-e60519b80b96.PNG)


## Checkpoint 4: What Did We Miss?
1. Select movies from hello-world with 
    ```
    curl -X POST admin:password@localhost:5984/hello-world/_find -d '{
       "selector": {
          "year": {
             "$gt": 1987
        }
      }
    }' -H 'Content-Type: application/json'
    ```
    Generates the output:
    ![4OneSelectMovies](https://user-images.githubusercontent.com/49171429/182275261-7eb62f75-c45f-4d07-9526-9bca0c1e165f.PNG)
    Without any errors.

2. Selecting Movies that come after `L` with the following command:
```
curl -X POST admin:admin@localhost:5984/hello-world/_find -d 
{
  \"selector\":
  {\"title\": {\"$gt\": \"L\"}}
} 
-H "Content-Type: application/json"
```
![CheckFourTwo](https://user-images.githubusercontent.com/49171429/182276956-27629f91-f6e4-48bb-823c-69e5f7cbc589.PNG)

3. Creating Index using the command:
```
curl -X POST admin:admin@localhost:5984/hello-world/_index -d "{\"index\": {\"fields\": [\"title\"]},\"name\": \"title-json-index\",\"type\": \"json\"}" -H "Content-Type: application/json"
```

![FourThree](https://user-images.githubusercontent.com/49171429/182277716-8c547df0-6417-47c8-a030-5f01f233535c.PNG)
![FourThreeResult](https://user-images.githubusercontent.com/49171429/182277802-00266fdb-acbe-48bb-b710-1555a2f2bf48.PNG)

4. Verify movie title query. Results:
![CheckFourFour](https://user-images.githubusercontent.com/49171429/182278088-39f33d28-e36a-4084-b903-e6d69da8ea88.PNG)
