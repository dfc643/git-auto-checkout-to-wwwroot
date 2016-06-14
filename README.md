Auto-checkout website from repo to wwwroot
=====

##Code
```bash
#!/bin/sh
GIT_TIMMER=`date +%s%N`
#------------- Modify by your repo ----------------
GIT_BRANCH=master
WEB_GIT_DIR=/var/git/repositories/git-test.git
WEB_WWW_DIR=/var/www/www.exmaple.com
#--------------------------------------------------
WEB_TMP_DIR=/tmp/git.web.$GIT_TIMMER

mkdir $WEB_TMP_DIR
sudo -u www-data rm -rf $WEB_WWW_DIR/*
git --work-tree=$WEB_TMP_DIR --git-dir=$WEB_GIT_DIR checkout $GIT_BRANCH -f
sudo -u www-data cp -R $WEB_TMP_DIR/* $WEB_WWW_DIR/
rm -rf $WEB_TMP_DIR/

echo Website has been up to date.
```

##Usage

1. Create a new file in your repositeory's ```hooks/post-receive.d``` folder.  
2. Copy the above script to the new file.  
3. Modify your repo path and website path in the script.  
4. Give this script executable permission.
5. Using ```visudo``` allow user git use ```rm``` and ```cp``` command by user www-data
