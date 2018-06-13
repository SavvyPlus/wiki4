<!-- TITLE: Python Libraries -->
<!-- SUBTITLE: A quick summary of Python Libraries -->


# <span id="title-text">IT Procedures : Python Libraries</span>

</div>

<div id="content" class="view">


<div id="main-content" class="wiki-content group">

This page describes the Python installation against which the various applications run. The list of libraries is up to date as at 10 May 2017.

### Python Version

All applications are compiled using Python 2.7.5

Full version details are Python 2.7.5 (default, May 15 2013, 22:43:36) MSC v 1.5000 32 bit (Intel)  on win32

Python's backward compatibility is pretty good so later versions of Python 2.x and/or other libraries should work ok. Note that Python 2.x and Python 3.x are separate languages with different syntax; code written for Python 2 will not work on Python 3.

### Installed Libraries

Here is a list of installed Python libraries. Most are part of the Python(x, y) distribution but a few have been added for various projects, most notably the web portal. The list is a result of running _pip freeze_ from the command line.

I have tried to highlight:

*   <span style="color: rgb(0,0,255);">in blue</span> required libraries that are not part of the base Python(x, y) installation
*   <span style="color: rgb(255,153,0);">in orange</span> libraries that are not part of Python(x, y) but I don't believe are required for any of our applications

-curses==2.2  
APScheduler==2.1.2  
Babel==1.3  
BeautifulSoup==3.2.1  
Bottleneck==0.7.0  
<span style="color: rgb(0,0,255);">Django==1.9.2</span>  
<span style="color: rgb(255,204,0);">Elixir==0.7.1</span>  
Fabric==1.8.0  
Jinja2==2.7.1  
MarkupSafe==0.18  
<span style="color: rgb(255,204,0);">MySQL-Connector-Python==1.1.5</span>  
<span style="color: rgb(255,204,0);">MySQL-python==1.2.4b4</span>  
Pillow==2.2.1  
PyICU==1.5  
PyInstaller==3.1.1  
PyOpenGL==3.0.2  
PyOpenGL-accelerate==3.0.2  
PyYAML==3.10  
Pygments==1.6  
SQLAlchemy==0.8.4  
Sphinx==1.2  
Tempita==0.5.1  
VTK==5.10.1  
ViTables==2.1  
Whoosh==2.5.5  
apptools==4.2.0  
astroid==1.0.1  
astropy==0.3  
backports.ssl-match-hostname==3.4.0.2  
beautifulsoup4==4.3.2  
blockcanvas==4.0.3  
cchardet==0.3.5  
<span style="color: rgb(0,0,255);">cdecimal==2.3</span>  
<span style="color: rgb(0,0,255);">ceODBC==2.0.1</span>  
certifi==0.0.8  
cffi==1.9.1  
chaco==4.3.0  
charade==1.0.3  
codetools==4.1.0  
colorama==0.3.1  
configobj==4.7.2  
<span style="color: rgb(0,0,255);">configparser==3.3.0r2</span>  
cov-core==1.7  
coverage==3.7.1  
cryptography==1.7.2  
cssselect==0.9.1  
cx-Freeze==4.3.2  
datrie==0.6.1  
decorator==3.4.0  
diff-match-patch==20121119  
<span style="color: rgb(0,0,255);">django-admin-bootstrapped==2.2.0</span>  
<span style="color: rgb(0,0,255);">django-autocomplete-light==3.0.4</span>  
<span style="color: rgb(0,0,255);">django-colorful==1.2</span>  
<span style="color: rgb(0,0,255);">django-concurrency==1.0.1</span>  
<span style="color: rgb(0,0,255);">django-debug-toolbar==1.2.1</span>  
<span style="color: rgb(0,0,255);">django-mssql==1.7</span>  
<span style="color: rgb(0,0,255);">django-pyodbc==0.3.0</span>  
<span style="color: rgb(0,0,255);">django-pyodbc-azure==1.9.1.0</span>  
<span style="color: rgb(0,0,255);">django-querysetsequence==0.6.1</span>  
<span style="color: rgb(0,0,255);">django-reversion==1.8.4</span>  
<span style="color: rgb(0,0,255);">django-sqlserver==1.7</span>  
<span style="color: rgb(0,0,255);">django-tinymce==2.3.0</span>  
docutils==0.11  
ecdsa==0.10  
ed25519ll==0.6  
enable==4.3.0  
encore==0.4.0  
enum34==1.0  
envisage==4.3.0  
ets==4.3.0  
etsdevtools==4.0.2  
etsproxy==0.1.2  
faulthandler==2.3  
formlayout==1.0.15  
funcsigs==0.4  
futures==2.1.6  
gevent==1.0  
gevent-websocket==0.9  
graphcanvas==4.0.2  
greenlet==0.4.1  
guidata==1.6.1  
guiqwt==2.3.1  
h5py==2.2.0  
html5lib==0.99  
idna==2.2  
imageio==0.4.1  
ipaddress==1.0.18  
ipdb==0.8  
ipdbplugin==1.4  
ipython==1.2.0  
jdcal==1.0  
keyring==3.3  
logilab-common==0.60.0  
lxml==3.3.5  
mahotas==1.0.3  
matplotlib==1.3.1  
mayavi==4.3.0  
mock==1.0.1  
nose==1.3.0  
nose-cov==1.6  
nose-fixes==1.3  
numexpr==2.3  
numpy==1.8.1  
openpyxl==2.0.3  
pandas==0.14.0  
paramiko==1.12.0  
pathlib==1.0  
<span style="color: rgb(255,204,0);">pdfminer==20140328</span>  
pep8==1.5.7  
petl==0.24.3  
ply==3.4  
psutil==1.2.1  
py==1.4.20  
py2exe==0.6.9  
pyMinuit==1.2.1  
pyOpenSSL==16.2.0  
pyasn1==0.1.9  
pycparser==2.17  
pycrypto==2.6  
pyemf==2.0.0  
pyface==4.3.0  
pyflakes==0.7.3  
pylint==1.0.0  
<span style="color: rgb(255,204,0);">pymongo==2.7.2</span>  
pyodbc==3.0.10  
pyparsing==2.0.1  
pyreadline==2.0  
python-dateutil==2.2  
pytz==2014.3  
pywin==0.3.1  
pywin32==218  
pyzmq==14.0.1  
reportlab==2.7  
requests==2.13.0  
rope==0.9.4  
sampy==1.2.1  
scimath==4.1.2  
scipy==0.13.3  
simplejson==3.5.2  
singledispatch==3.4.0.3  
six==1.10.0  
smc.freeimage==0.3dev  
spyder==2.2.5  
sqlalchemy-migrate==0.8.2  
sqlparse==0.1.12  
tables==3.0.0  
tornado==3.1.1  
traits==4.3.0  
traitsui==4.3.0  
urllib3==1.20  
veusz==1.19.1  
virtualenv==1.10.1  
virtualenvwrapper-win==1.1.5  
wheel==0.22.0  
wincertstore==0.1  
wsaccel==0.6.2  
wxPython==2.8.12.1  
wxPython-common==2.8.12.1  
xlrd==0.9.3

### Application Packaging

For building applications I am using PyInstaller (version 2.1)

Documentation is available at [http://www.pyinstaller.org/](http://www.pyinstaller.org/) which includes troubleshooting hints

</div>

</div>

</div>

<div id="footer" role="contentinfo">

<section class="footer-body">



</section>

</div>

</div>