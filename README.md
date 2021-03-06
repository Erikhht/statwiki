# statwiki
**Automatically exported from http://code.google.com/p/statwiki**

## About 

This is a trimmed down Wiki engine, that generates static HTML files from _wikitext_ (.wiki files).

Although a static wiki might strike you as an obvious oxymoron, the idea is the content is managed by an external tool (typically a code versioning system such as CVS or Subversion), rather than by the Wiki engine itself.

This was inspired from Google Code Wiki, and is aimed to be used in open-source hosting services such as SourceForge or Berlios, which provide code versioning systems, but where the usage Wiki is either not supported or encumbered by several aspects.

Doing so has several advantages:

  * No files are written, or databases accessed by the web server, so no need for world writeable directories, or world readable passwords.
  * Edit access is given by the repository commit access, so the access control is not duplicated.
  * It can be used off-line.

And of course, disadvantages:

  * There is no web interface for editing and previewing the wiki pages.
  * No dynamic content means the site navigation is much poorer.

The Wiki engine was adapted from the [MoinMoin Wiki engine](http://moinmoin.wikiwikiweb.de/) written in Python. Changes were:

  * Eliminate all the dynamic stuff, to ensure page content does not depend on other pages:
    * macros
    * plug-ins
    * cross-reference links
  * Eliminate all but the necessary code:
    * theming (look is only controlled by CSS)
    * multiple input/output formats
    * etc.
  * Slightly modify the syntax to match Google's Code Wiki Syntax (which is more intuitive in my opinion)
  
## Code license
[GNU GPL v2](http://www.gnu.org/licenses/old-licenses/gpl-2.0.html)

## Usage

Just run the `statwiki.py` with the `--make` option in the directory containing the `*.wiki` files and the corresponding HTML files will be generated.

For a complete list of possible options, start it with `--help` option.

## Syntax 

The Wiki syntax is the same as Google Code as is described in http://code.google.com/p/support/wiki/WikiSyntax.

## Using with SourceForge and Subversion

First create a folder for the wiki in subversion:
```
svn mkdir https://PROJECTNAME.svn.sourceforge.net/svnroot/PROJECTNAME/wiki
```
Add the default.css and the content to the wiki.

Checkout the wiki content from within the SourceForge shell:
```
ssh shell.sourceforge.net
cd /home/groups/P/PR/PROJECTNAME/htdocs
svn co https://PROJECTNAME.svn.sourceforge.net/svnroot/PROJECTNAME/wiki
```
Put the statwiki source code somewhere.
```
scp -pr statwiki/ shell.sf.net:/home/groups/P/PR/PROJECTS/statwiki
```
Create a cronjob:
```
#!/bin/sh

set -e

GROUP=/home/groups/P/PR/PROJECTNAME
WIKI=$GROUP/htdocs/wiki
STATWIKI=$GROUP/statwiki/statwiki.py

cd $WIKI
svn -q update > /dev/null
$STATWIKI --make > /dev/null
```
## Examples

You can see a live example of a site generated by statwiki in http://arkadiusz.wahlig.eu or http://idc.sourceforge.net/.

## Download

  * Subversion repository

## Links

Other wikis with subversion backend support:

  * http://jspwiki.org/
  * http://ikiwiki.info/
