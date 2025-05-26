---
layout: single
permalink: /computing/
---

# Computing

## Warwick SCRTP

### Basics

- Register for an account [here](https://warwick.ac.uk/research/rtp/sc/desktop/gettingstarted/).
- Documentation is [here](https://docs.scrtp.warwick.ac.uk/). Use your Warwick id/pass to get in.
- Methods to connect are under SCTRP Linux/Remote access. If you don't know what ssh is, the web browser access is probably simplest.
- Log into my machines vega1.astro.warwick.ac.uk or betapic.astro.warwick.ac.uk (do not use the shared gateway machine godzilla).
- The terminal is the main way to do things on the machines, open one by double clicking on the icon on the desktop.
- There is some information on the Linux command line (terminal) in the Docs under General information.

### Loading modules

When logging in to SCRTP machines, run the command below in a terminal to get access to python and some necessary modules. This will allow you to run a jupyter notebook too.

<code>module load GCC/11.3.0  Python/3.10.4 IPython/8.5.0  FFTW/3.3.10 OpenMPI/4.1.4 astropy/5.1.1 matplotlib/3.5.2 h5py/3.7.0 CMake/3.24.3</code>

If you then type `module save`, you can restore the configuration next time with `module restore` (rather than pasting the whole command in each time).


### Python

If you need python modules that don't exist in (e.g. you get import errors), you can install these with something like `pip install --user rebound`. This puts them in a hidden folder in your home space. You will need to have restored the modules above for this to work.

Having loaded the modules, open a jupyter notebook by typing `jupyter notebook`. This will open a browser window with the jupyter file browser, use this to find and then run your notebook.

### Running long jobs

You can run code that will take a while by using `screen`. Typing `screen` in a terminal will open a new terminal session in that window (you will need to type `module restore` again). Here you can start a piece of code and then exit with `ctrl-a d`. The terminal is still running but you can leave (e.g. close the brower or terminal window) and come back later with `screen -r`.

## Mac setup

<p>My list of software to get a new mac up to speed. Latest was el Capitan.</p>



<ul>
	<li>Run software update</li>
	<li>Sign into iCloud, turn everything but Notes off</li>
	<li>Check shell is zsh in System Preferences (apparently default?)</li>
	<li>Various finder preferences, e.g. filename extensions</li>
	<li>Turn on FileVault, Firewall</li>
	<li>Chrome</li>
	<li>Office</li>
	<li>Xcode (also xcode-select --install)</li>
	<li>Slack</li>
	<li>x2go</li>
	<li>MacTex and BibDesk (use TeX Live Utility to do updates and check paper size )</li>
	<li>XQuartz</li>
	<li>homebrew (this involved cloning homebrew-core on a different machine with institutional internet and copying it into place)</li>
	<li><a href="https://tech-cookbook.com/2021/10/25/how-to-setup-mamp-macos-apache-mysql-php-on-macos-12-monterey-2021/">web server</a>, homebrew httpd, homebrew php, mysql
	 <ul>
	 	<li>copy tables using <a href="http://stackoverflow.com/questions/9497869/export-and-import-all-mysql-databases-at-one-time">mysqldump</a>, mysql -uuser -ppass -N -e &#8220;show databases like &#8216;%&#8217;;&#8221; |grep -v -F mysql |grep -v -F _schema|grep -v -F sys |xargs mysqldump -uuser -ppass &#8211;databases > alldb.sql, and read back in with &#8211;force option if version related errors.</li>
	 </ul></li>
	 <li><a href="http://www.sequelpro.com/">Sequel Pro</a> (buggy, latest test build seems fine)</li>
	 <li><a href="http://www.onekilopars.ec/iobserve/">iObserve</a></li><li>Sublime Text</li>
	 <li><a href="http://www.star.bris.ac.uk/~mbt/topcat/">Topcat</a> and the stilts script
	 	<ul>
	 		<li>add /Library/Java/Extensions/<a href="https://dev.mysql.com/downloads/connector/j/">mysql-connector-java-X.X.X-bin.jar</a> for MySQL compatibility</li>
	 		<li>Java</li>
	 	</ul></li>
 	<li>cdsclient (had to compile and place wwwget to /usr/local/bin by hand)</li>
 	<li><a href="https://pypi.org/project/ads2bibdesk/">ads2bibdesk</a> (and <a href="https://ads.readthedocs.io/en/latest/">ads</a>)
 		<ul>
 			<li>comment line ~287 in python script to use bibcodes as cite key</li>
	 		<li>service doesn&#8217;t work, but terminal OK</li>
	 	</ul></li>
	 <li><a href="https://johannesbuchner.github.io/PyMultiNest/index.html">(py)multinest</a></li>
  <ul>
  <li> may need to do: export FCFLAGS="-w -fallow-argument-mismatch -O2" and
  export FFLAGS="-w -fallow-argument-mismatch -O2" for make to work</li>
  </ul>   
	 <li><a href="https://mtazzari.github.io/galario/">galario</a></li>
	 <li><a href="https://sites.google.com/cfa.harvard.edu/saoimageds9/home">DS9</a></li>
</ul>


### Installing galario

Steps to install [galario](https://mtazzari.github.io/galario/) on SCRTP and Mac.

- For SCRTP import modules, e.g. module load GCC/8.3.0  OpenMPI/3.1.4 Python/3.7.4 FFTW/3.3.8 CMake/3.15.3 IPython/7.9.0-Python-3.7.4
- For Mac install these with homebrew, and probably need to specify homebrew gcc/g++ when calling cmake.
- Follow instructions <a href="https://mtazzari.github.io/galario/install.html">here</a>, including python binding
- Example for Mac: cmake -DCMAKE_C_COMPILER=/usr/local/bin/gcc-11 -DCMAKE_CXX_COMPILER=/usr/local/bin/g++-11 -DPython_ADDITIONAL_VERSIONS=3.9 ..
- Find python site-packages, create galario directory, and copy contents 
of galario/build/python/galario (single, double, \_\_init\_\_.py) into it.
- For example; cp -r python/galario/* ~/.local/lib/python3.7/site-packages/galario/

To use galario with emcee, set the number of galario threads to 1 with galario.double.threads(num=1). It won&#8217;t work otherwise.
