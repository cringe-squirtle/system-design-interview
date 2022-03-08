
# Google Drive

### Requirement
- personal drive
- folders, files
- CRUD, downloading
- sync 10s updates - pull getFile/Folder every 10s or pub/sub system
- 1B users (15 GB / user)

### Operation
- create a folder
- upload/download file 
- move, delete, rename, get file/folder

### Note
- file related - blob storage - Google Cloud Server, or AWS S3

### server

- createFolder
  - client -> Load balancer -> multi key-value blob store
  - store columns: ID, name, ownerID, children:[], isFolder:boolean, parent, blobs
- storage
  - 1000^3 * 15 ≈ 15 000 Petabytes
  - +replicas 15,000 * 3 ≈ 50,000 petabytes
- uploadFile
  - client -> Load balancer (round-robin) -> multi blob stores 
  - hash content as adress - content -> hashedKey -> {key: hashedKey, point_to: content}
  - in order to have no duplicated data uploaded multiple times even by different users
  - concept: content addressable storage
  - continued graph
    - multi blob stores -> load balancer (blob hashing, compressing, caching) -> blob stores  
- download
  - go to folder, find blob, get content
- moving
  - update folder parent
- delete
  - delete folder children, and blobs
