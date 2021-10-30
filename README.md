## Setup
Create SSH key and copy the public key
``` 
ssh-keygen -t rs
cat /home/ec2-user/.ssh/id_rsa.pub
```

## Create a new Hugo Site

Create a new Hugo site in the current directory
```hugo new site . --force```

### Add a theme
```
git submodule add https://github.com/budparr/gohugo-theme-ananke.git themes/ananke
echo 'theme = "ananke"' >> config.toml
```