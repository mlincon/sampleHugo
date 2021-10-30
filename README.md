## Setup

### Setup Hugo
Download the _extended_ version of Hugo and put it in the `~/bin/` folder. Here version `0.88.1` is used.
```
wget https://github.com/gohugoio/hugo/releases/download/v0.88.1/hugo_extended_0.88.1_Linux-64bit.tar.gz
tar xzvf hugo_extended_0.88.1_Linux-64bit.tar.gz
mv ~/environment/hugo ~/bin/hugo
```

Check installation
```
which hugo
hugo version
```

### SSH key for Github
Create SSH key and copy the public key
``` 
ssh-keygen -t rs
cat /home/ec2-user/.ssh/id_rsa.pub
```

### EC2 Port
Add a new security group to the EC2 and open port `8080` to all incoming traffic.


### S3 Bucket Policy for Public Content
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": [
                "s3:GetObject"
            ],
             "Resource": [
                "arn:aws:s3:::<unique-bucket-name>/*"
            ]
        }
    ]
}
```



## Create a new Hugo Site

Create a new Hugo site in the current directory
```hugo new site . --force```

### Add a theme
```
git submodule add https://github.com/budparr/gohugo-theme-ananke.git themes/ananke
echo 'theme = "ananke"' >> config.toml
```

### Add new content
```
hugo new posts/foobar.md
```

### Check current IP
```
curl ipinfo.io
```

### Start hugo server
Using the IP from the above step, run
```
hugo serve --bind=0.0.0.0 --port=8080 --baseURL=http://<my-ip>/
```
Click on the provided link.

### Generate static pages
Simply run `hugo` to generate the required static files. The static files are available in the `public` folder.
