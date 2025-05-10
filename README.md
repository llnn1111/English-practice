# English-practice
## Features

## Content Ingestion Functionality <!-- by [Dragonfly] -->

CatraMMS provides a flexible content ingestion pipeline supporting multiple ingestion methods:

### 1. **Local File Upload**
Users can upload local files through a simple file picker interface. The script example at `CatraMMS/scripts/examples/ingestOfImage/helper/ingestionWorkflow.sh` demonstrates this operation, requiring users to configure:
- User/API keys for authentication
- Metadata (title, tags, retention policy)
- File format validation

Command example:
```bash
if [ $# -ne 8 ]; then
    echo "Usage: $0 <mmsUserKey> <mmsAPIKey> <title> <tag> <ingester> <profileset> <retention> <fileFormat> ($#)"
    exit 1
fi

mmsAPIHostName=mms-api.cibortv-mms.com
mmsUserKey=$1
mmsAPIKey=$2
title=$3
tag=$4
ingester=$5
profileSet=$6
retention=$7
fileFormat=$8

sed "s/\${title}/$title/g" ./helper/ingestionWorkflow.json | sed "s/\${tag}/$tag/g" | sed "s/\${ingester}/$ingester/g" | sed "s/\${profileSet}/$profileSet/g" | sed "s/\${retention}/$retention/g" | sed "s/\${fileFormat}/$fileFormat/g" > ./helper/ingestionWorkflow.json.new

responseCode=$(curl -o ./helper/ingestionWorkflowResult.json -w "%{response_code}" -k -s -X POST -u $mmsUserKey:$mmsAPIKey -d @./helper/ingestionWorkflow.json.new -H "Content-Type: application/json" https://$mmsAPIHostName/catramms/1.0.1/workflow)
if [ "$responseCode" -ne "201" ]; then
    echo "$(date +%Y-%m-%d-%H:%M:%S): FAILURE, Ingestion response code: $responseCode"
    exit 2
fi

rm ./helper/ingestionWorkflow.json.new

#print ingestionJobKey
jq '.tasks[] | select(.type == "Add-Content") | .ingestionJobKey' ./helper/ingestionWorkflowResult.json
![alt text](images/图像上传.png)
![alt text](images/视频上传.png)

### 2. **Cloud Storage Integration**
Supports direct content import from third-party cloud providers (e.g., Google Drive, Dropbox) via sourceURL configuration. While no specific cloud SDKs are used, the system supports fetching content from external storage URLs:
"parameters": {
    "sourceURL": "http://myhost/example.mp4",  // Supports HTTP/HTTPS/FTP/FTPS protocols
    // ...
}


### 3. **Batch Import**
Allows users to import multiple files at once, supporting various file formats. The script at CatraMMS/scripts/examples/ingestionOfStreamingURL/ingestionOfStreamingURL.sh demonstrates batch import by processing files containing multiple titles and streaming URLs sequentially:
if [ $# -lt 8 ]; then
    echo "Usage: $0 <mmsUserKey> <mmsAPIKey> <tag> <ingester> <retention> <encodersPool> <encodingProfilesSet> <streamingURLFile>"
    echo "The current parameters number is: $#, it shall be 9"
    paramIndex=1
    for param in "$@"
    do
        echo "Param #$paramIndex: $param";
        paramIndex=$((paramIndex + 1));
    done
    exit 1
fi

mmsUserKey=$1
mmsAPIKey=$2
tag=$3
ingester=$4
retention=$5
encodersPool=$6
encodingProfilesSet=$7
streamingURLFile=$8

mmsAPIHostName=mms-api.catramms-cloud.com

while read titleAndtreamingURL; do
    if [ "$titleAndtreamingURL" = "" ]; then
        continue
    fi

    title=$(echo $titleAndtreamingURL | cut -d ";" -f 1)
    streamingURL=$(echo $titleAndtreamingURL | cut -d ";" -f 2)
    encodedStreamingURL=${streamingURL//\//"\\/"}
    encodedStreamingURL=${encodedStreamingURL//\&/"\\&"}

    sed "s/\${title}/$title/g" ./helper/ingestionWorkflow.json | sed "s/\${streamingURL}/$encodedStreamingURL/g" | sed "s/\${tag}/$tag/g" | sed "s/\${ingester}/$ingester/g" | sed "s/\${retention}/$retention/g" | sed "s/\${encodersPool}/$encodersPool/g" | sed "s/\${encodingProfilesSet}/$encodingProfilesSet/g" > ./helper/ingestionWorkflow.json.new
    curl -o ./helper/ingestionWorkflowResult.json -k -s -X POST -u $mmsUserKey:$mmsAPIKey -d @./helper/ingestionWorkflow.json.new -H "Content-Type: application/json" https://$mmsAPIHostName/catramms/1.0.1/workflow
done < "$streamingURLFile"
![alt text](images/批量上传.png)

### 4. ** Automated Ingestion**
Implements scheduled ingestion through:
  Filesystem monitoring: Initially designed using incrontab (inotify-based), later adapted to use cron-triggered scripts due to mounted directory limitations
  Watch folder pattern: Periodically scans designated directories for new files
  
