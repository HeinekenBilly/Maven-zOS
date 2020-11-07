
## Table of Contents

* [Maven on zOS](#about-the-project)
* [Prerequisites](#prerequisites)
* [Settings](#settings)


## Maven on zOS


Yes, you can use Maven on zOS under USS, reason being maven at end of the day is Java application and require JRE which is available on USS for most installation. This took me a full week to figure it out but it worked eventually. 

### Prerequisites

1. Access to OMVS shell. 

2. You will need Maven binaries in zipped format and can be downloaded from [here](https://mirrors.estointernet.in/apache/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.zip)

3. Unzip the binaries to any location on your workstation and then transfer using IBM Idz or any other method available to your home direcorty of USS or any other location of your choice. 

4. If you have cURL for zOS which comes packaged with Rocket Git, you can directly download on to USS. 

### Settings

1. CD to your direcory where you kept the files on USS and run the following command
```sh 
chtag -tc ibm-1047 ~/apache-maven-3.6.3/bin/m2.conf 
```
2. Now make a copy of this file, just in case. 
```sh
cp ~/apache-maven-3.6.3/bin/m2.conf ~/apache-maven-3.6.3/bin/m2.conf.bkp
```
3. Rename the m2.conf to m2.conf.old
```sh
mv m2.conf m2.conf.old
```
4. Now using iconv to change the encoding of m2.conf to UTF-8
```sh
iconv -f ibm-1047 -t UTF-8 ~/apache-maven-3.6.3/bin/m2.conf.old > ~/apache-maven-3.6.3/bin/m2.conf
```
5. set MAVEN_OPTS to use UTF-8 encoding, remember that is zOS so default encoding is Ebcidc.
```sh
export MAVEN_OPTS=-Dfile.encoding=UTF-8
```
6. Set execute permission on ~/apache-maven-3.6.3/bin.mvn
```sh
chmod +x ~/apache-maven-3.6.3/bin/mvn
```
7. Test Drive should show version instead of hieroglyph. 
```sh
mvn -v
```

With Love,
Billy 'The Cat'
