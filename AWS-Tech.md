### Save the file in String
 ```    
    ObjectMetadata objectMetadata = metadata != null ? metadata : new ObjectMetadata();
    objectMetadata.setContentType("text/plain");
    byte[] objectByteArray = IOUtils.toByteArray(inputStream);
    objectMetadata.setContentLength(objectByteArray.length);
    this.s3.putObject(bucketName, key, new ByteArrayInputStream(objectByteArray), objectMetadata);
```  
#### Save CSV file 
    
   ```
    final File tmpFile = File.createTempFile(filePrefix, ".csv");
    String outText = Strings.join(leaf_topic, valuesList.get(verb_text_index));
    FileUtils.writeStringToFile(tmpFile, outText, true);
    FileUtils.writeStringToFile(tmpFile, "\n", true);
    s3Client.addObject(s3Bucket, s3ObjectName + filePrefix + ".csv", tmpFile);
   ```
#### Object exist or not

```  
    s3.doesBucketExist(bucketName) && s3.doesObjectExist(bucketName, key);

```
### Get Object 
 
 ```
    S3Object s3Object = s3Client.getObject(bucket, key);
    InputStream objectData = s3Object.getObjectContent();
    String text = IOUtils.toString(objectData, StandardCharsets.UTF_8.name());

 ```

###   Get Url bucket
```
    expirationTimeInSec =  configService.getInt("s3.objectURLExpiration");
    Date expiration = new Date();
    long msec = expiration.getTime();
    msec += 1000 * expirationTimeInSec;
    expiration.setTime(msec);
    GeneratePresignedUrlRequest generatePresignedUrlRequest = new GeneratePresignedUrlRequest(bucketName, key);
    generatePresignedUrlRequest.setMethod(HttpMethod.GET);
    generatePresignedUrlRequest.setExpiration(expiration);

    return s3.generatePresignedUrl(generatePresignedUrlRequest).toString();

```


    
