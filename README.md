# cleanup-in-ISLE-one-please
Obliterates unnecessary directories and files found in Islandora/ISLE.

## Attention!  
If you found this file and/or one named `OBLITERATED.md` lurking inside your Islandora stack, then it was put here to replace some files/folders that were deemed "unnecessary".  If you're confused by this statement, please read on.

*Use this module with caution!*  It has been, and continues to be, tested with ISLE instances of Islandora, but there's always the possibility that it might obliterate something you really do need.

## Overview
This project introduces a `docker-compose.override.yml` file that essentially _obliterates_ unnecessary files and folders by replacing them with this project...which essentially does *NOTHING* but present this explanation in this `README.md` document along with a second Markdown document named `OBLITERATED.md`.

## Why Do I Need This?
If you have ever peeked under the hood at Islandora, or more specifically, at FEDORA and FGSearch, you may have seen confusing directory structures and repetition like this example:

```
root@9c166be40ab6:/# find /usr/local/tomcat -name foxmlToSolr.xslt
/usr/local/tomcat/webapps/fedoragsearch/FgsConfig/DrupalModuleForIslandora/islandora_gsearch/FgsConfigIndexTemplate/Solr/foxmlToSolr.xslt
/usr/local/tomcat/webapps/fedoragsearch/FgsConfig/FgsConfigIndexTemplate/Solr/foxmlToSolr.xslt
/usr/local/tomcat/webapps/fedoragsearch/FgsConfig/configDemoOnSolr/index/FgsIndex/foxmlToSolr.xslt
/usr/local/tomcat/webapps/fedoragsearch/FgsConfig/configForIslandora/fgsconfigFinal/index/FgsIndex/foxmlToSolr.xslt
/usr/local/tomcat/webapps/fedoragsearch/WEB-INF/classes/fgsconfigFinal/index/FgsIndex/foxmlToSolr.xslt
```
Hmmm, 5 copies of the same file?  Which one is "significant" and in-control?  Are the others even necessary?  What happens if I remove the "others"?

I cannot definitively answer the last two questions... hence the note about using this module with CAUTION!  However, this module can help you do some investigation, and maybe save your sanity if/when you do encounter any duplicates like this, or you positively identify a file/folder that is just useless cruft.

## How Does This Work?
This module assumes that you're working in an ISLE (https://github.com/Islandora-Collaboration-Group/ISLE) instance of Islandora, one that uses `Docker` and `docker-compose`.  In that case you have a `docker-compose.yml` file that holds the key to your configuration; it's the file that is responsible for ultimately building your Islandora/ISLE stack.  You can easily override portions of your stack configuration using a file named `docker-compose.override.yml`, and a sample/template of one such file is included in this project.  

When you issue a `docker-compose up -d` from the ISLE folder on your host (the directory that your `docker-compose.yml` file is in) any `docker-compose.override.yml` file found in that same folder will be *automatically* processed.  An explantion of how all this works can be found in https://docs.docker.com/compose/extends/.

## How Is This Used?
It's easy, just follow these steps...

  1) Open a terminal to your ISLE host, and in that terminal...  
  2) Navigate (`cd`) your working directoy to ISLE, the directory that holds your `docker-compose.yml` file.  
  3) `git clone` this repository to your ISLE host with something like `git clone https://github.com/DigitalGrinnell/cleanup-in-ISLE-one-please.git`  
  4a) If you already have a `docker-compose.override.yml` file in your working directory, MERGE the contents of `./cleanup-in-ISLE-one-please/docker-compose.override.yml` into it.  
  4b) If you do NOT already have a `docker-compose.override.yml` file, just copy the sample included here like so: `cp ./cleanup-in-ISLE-one-please/docker-compose.override.yml .`  
  5) Edit the `docker-compose.override.yml` that's now in your working directory.  If you used the sample file from this project you'll find editing instructions inside the file.  If you already had your own `docker-compose.override.yml` please look at this project sample for guidance IF you don't already understand what to do.  
  6) Once your `docker-compose.override.yml` is complete spin up your ISLE stack with `docker-compose up -d` as usual.
