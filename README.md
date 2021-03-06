Simple Dropbox Uploader
===

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Dropbox uploader. Take what you want from `stdin` and put to DropBox using API v2.

> #### :warning: I write **Simple Dropbox Uploader** (1 file - 50 rows) mainly for my purposes, having found nothing like it. Not tested. If you are looking for a better project try [Dropbox Uploader](https://github.com/andreafabrizi/Dropbox-Uploader)

Based on [this](https://github.com/dropbox/dropbox-sdk-python/tree/main/example/back-up-and-restore) dropbox-api example.


## Install
```
docker pull massimorebuglio/simple-dropbox-uploader
export SDU_DROPBOX_TOKEN=YourSecretToken
```

## Examples

#### Upload text file
```
echo 'Ciao!' >> ciao.txt
cat ciao.txt | \
  sudo docker run -i massimorebuglio/simple-dropbox-uploader \
  -n /ciao_on_dropbox.txt -t $SDU_DROPBOX_TOKEN
```

#### Backup text file with datetime information
```
echo 'Ciao!' >> ciao.txt
cat ciao.txt | \
  sudo docker run -i massimorebuglio/simple-dropbox-uploader \
  -n /ciao.backup.$(date +%F_%R).txt -t $SDU_DROPBOX_TOKEN 
```

#### Backup folder
```
tar -czvf - /path/to/folder | \
  sudo docker run -i massimorebuglio/simple-dropbox-uploader \
  -n /folder.backup.$(date +%F_%R).tar.gz -t $SDU_DROPBOX_TOKEN 
```

#### Backup mongodb running in a docker container
```
sudo docker exec MONGO_CONTAINER_NAME \
  sh -c 'mongodump --authenticationDatabase admin -u MONGO_USERNAME -p MONGO_PASSWORD --archive' | \
  sudo docker run -i massimorebuglio/simple-dropbox-uploader \
  -n /mongo.backup.$(date +%F_%R).dump -t $SDU_DROPBOX_TOKEN 
```









