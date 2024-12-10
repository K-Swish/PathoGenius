# PathoGenius
A Filoviridae Ebolavirus Genome database


Find all other info here: https://k-swish.github.io/PathoGenius/

## Instalation:
To install, please ensure you already have a functioning Apache2 web server. 

Apache2 web servers serve files from within a root directory. For a normal linux installation, the folder should be /var/www or /var/www/html, whereas when you install on macOS using brew it will likely be in /opt/homebrew/var/www (for M1) or /usr/local/var/www (for Intel). Set APACHE_ROOT to the path to your root directory.
```
export APACHE_ROOT='/path/to/rootdir'
```
Then, make a temporary directory as a staging area.
```
mkdir ~/tmp
cd ~/tmp
```
Download and copy over jbrowse2 into your root directory and set the owner to the curent use (you)
```
jbrowse create output_folder
sudo mv output_folder $APACHE_ROOT/jbrowse2
sudo chown -R $(whoami) $APACHE_ROOT/jbrowse2
```
