## S3 Property config
```
accessKey=
secret=
region=
bucketName=
```

## S3 COnfiguration
```
    @Value("${accessKey}")
    private String accessKey;

    @Value("${secret}")
    private String secret;

    @Value("${region}")
    private String region;

    @Bean
    public AmazonS3 s3(){
        AWSCredentials awsCredentials=new BasicAWSCredentials(accessKey,secret);
        return AmazonS3ClientBuilder.standard().withRegion(region)
            .withCredentials(newAWSStaticCredentialsProvider(awsCredentials)).build();
    }
```

## S3 Operation

### File save
```
    @Value("${bucketName}")
    private String bucketName;

    @Autowired
    private  final AmazonS3 s3;
 
    public String saveFile(MultipartFile file) {
        String originalFilename = file.getOriginalFilename();
        int count = 0;
        int maxTries = 3;
        while(true) {
            try {
                File file1 = convertMultiPartToFile(file);
                PutObjectResult putObjectResult = s3.putObject(bucketName, originalFilename, file1);
                return putObjectResult.getContentMd5();
            } catch (IOException e) {
                if (++count == maxTries) throw new RuntimeException(e);
            }
        }
    }
    private File convertMultiPartToFile(MultipartFile file ) throws IOException
    {
        File convFile = new File( file.getOriginalFilename() );
        FileOutputStream fos = new FileOutputStream( convFile );
        fos.write( file.getBytes() );
        fos.close();
        return convFile;
    }

```

### S3 File download
```
 public byte[] downloadFile(String filename) {
        S3Object object = s3.getObject(bucketName, filename);
        S3ObjectInputStream objectContent = object.getObjectContent();
        try {
           return IOUtils.toByteArray(objectContent);
        } catch (IOException e) {
            throw  new RuntimeException(e);
        }
    }
```

### S3 File delete
```
 public String deleteFile(String filename) {
       s3.deleteObject(bucketName,filename);
        return "File deleted";
    }
```

### S3 list of files
```
public List<String> listAllFiles() {
   ListObjectsV2Result listObjectsV2Result = s3.listObjectsV2(bucketName);
   return listObjectsV2Result.getObjectSummaries().stream().map(S3ObjectSummary::getKey).collect(Collectors.toList());
 }
```
