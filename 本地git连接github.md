1. git config --global user.name "xonge"
   git config --global user.email xonge007x@sina.com
   
2. ssh-keygen -t rsa -C "xonge007x@sina.com"
   
3. host github
           hostname github.com
           user git
           identityfile ~/.ssh/github_xonge
           port 22