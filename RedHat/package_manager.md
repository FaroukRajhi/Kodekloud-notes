# Create a yum repo file located at /etc/yum.repos.d/kodekloud.repo as per details given below:

short name: KodeKloud

long name: KodeKloud - $basearch

baseurl: https://repos.kodekloud.com/linux/$releasever/$basearch/development


Also make sure it is set to be enabled.

sudo vi /etc/yum.repos.d/kodekloud.repo

[KodeKloud]
name=KodeKloud - $basearch
baseurl=https://repos.kodekloud.com/linux/$releasever/$basearch/development
enabled=1

# Using the correct command, display all of the possible package groups, including those that are hidden

sudo yum group list --hidden

# Using the correct command, display the available module streams for php

sudo yum module list php

