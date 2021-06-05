# ciriema

This Quarkus project allows you to run a CI pipeline strait from terminal, with an simple yaml configuration.

```
s+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
s+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
s+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
s+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
s+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
s+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
s++++++++++++++++++++++++++++++++++++++/////////////////////////////////++++++++++++++++++++++++++++
s++++++++++++++++//////////////////////////////////////////////////////////////////+++++++++++++++++
s+++++++///////////////////////////++//++///////////////////////////////////////////////++++++++++++
s+++++////////////////////////////++++oo++o//////////////////////////////////////////////+++++++++++
s//////////////////////////////+++++o+ss+so+////////////////////////////////////////////////////////
s/////////////////////////////////++syshsys+/////////////////////////////////////////////////////+//
s///////////////////////////////+syyyhddhhs+////////////////////////////////////////////////////////
s//////////////////////////////+dmmdddmdmmdho///////////////////////////////////////////////////////
s//////////////////////////////hNmdydmddho++////////////////////////////////////////////////////////
s/////////////////////////////+dmdhhddys+///////////////////////////////////////////////////////////
s/////////////////////////////+mmmddhs+/////////////////////////////////////////////////////////////
s/////////////////////////////+ddhyso+//////////////////////////////////////////////////////////////
s//////////////////////////////ydhso////////////////////////////////////////////////////////////////
s//////////////////////////////omhs+////////////////////////////////////////////////////////////////
s//////////////////////////////omdyo////////////////////////////////////////////////////////////////
s//////////////////////////////+mdys+///////////////////////////////////////////////////////////////
s//////////////////////////////+mdhy+///////////////////////////////////////////////////////////////
s//////////////////////////////ommmso+//////////////////////////////////////////////////////////////
s//////////////////////////////ommmyo++/////////////////////////////////////////////////////////////
s//////////////////////////////smmmyoo+++oo++++/////////////////////////////////////////////////////
s//////////////////////////////dmmmyoo++ooossyyssso+////////////////////////////////////////////////
s//////////////////////////////mmmmysooooooossssssssso//////////////////////////////////////////////
s//////////////////////////////mmmmyssossssooooooosssso+////////////////////////////////////////////
s/////////////////////////////+mmmhhhysssshsooo+++oooooooo+/////////////////////////////////////////
s/////////////////////////////+mmmhmmdyso+yhyooo++++++oooooso+//////////////////////////////////////
s//////////////////////////////hmmmmmmhyso+ohdhso+o++++ooo+osys+////////////////////////////////////
s//////////////////////////////ommmmmmmyso+///ohdhysooooooooosyhy+//////////////////////////////////
s///////////////////////////////ymmmmmmdyso+//:-:+ddyysoooossyyyhdh+////////////////////////////////
s////////////////////////////////sdmmmmmhhyo++/::::ohhhmhyhyyyyyyhhmy///////////////////////////////
s/////////////////////////////////+hdmmmhddhyoo/::::/yhdmmmmmmdhyyhdmdo/////////////////////////////
s///////////////////////////////////ohdmdmdmdyhs/:::+oshddddmmmmmdddddo/////////////////////////////
s/////////////////////////////////////+ymmmmdhhhy+:/+++oosydmmmdsssdNmo/////////////////////////////
s///////////////////////////////////////+hNd/++/+o+o///////ohddy+/+hmNs/////////////////////////////
s/////////////////////////////////////////hy//////s+////////oyyyo+sdmNdo////////////////////////////
s/////////////////////////////////////////+y//////+o+/////////++++dmNNNmh+//////////////////////////
s//////////////////////////////////////////o+//////s+/////////////omNNNNNd+/////////////////////////
s///////////////////////////////////////////y//////+s//////////////+mNNNNNmo////////////////////////
s///////////////////////////////////////////sd+/////so+/////////////+dNNNNNms///////////////////////
s////////////////////////////////////////////mds////syo+/////////////+dNNNNNmy//////////////////////
s///////////////////////////////////////////+mmh////hy++//////////////+hmmmmmdy+////////////////////
s////////////////////////////////////////////yds////ss//////////////////yddddddo////////////////////
s////////////////////////////////////////////sdo////o+///////////////////shdddho////////////////////
s////////////////////////////////////////////sy+////s/////////////////////+syys+////////////////////
s////////////////////////////////////////////oh+////s////////////////////////+//////////////////////
s////////////////////////////////////////////od+////s///////////////////////////////////////////////
s////////////////////////////////////////////om/////o///////////////////////////////////////////////
s////////////////////////////////////////////sm/////o///////////////////////////////////////////////
s////////////////////////////////////////////sd////++///////////////////////////////////////////////
s////////////////////////////////////////////sd////+////////////////////////////////////////////////
s////////////////////////////////////////////yh////o////////////////////////////////////////////////
s////////////////////////////////////////////hd////s////////////////////////////////////////////////
s/////////////////////////////////////////++ohmy+/+ho+//////////////////////////////////////////////
s/////////////////////////////////////oyhyhmdhmysyyds+//////////////////////////////////////////////
s///////////////////////////////////hyNNddmNNNmsydNhso+/////////////////////////////////////////////
s//////////////////////////////////+NNNmdNNNNNmydNhyys+/////////////////////////////////////////////
s//////////////////////////////////oNNNNmNNNmmhyyhyhhs+/////////////////////////////////////////////
s//////////////////////////////////oNNNmhNmdNNyysyhNNy//////////////////////////////////////////////
s//////////////////////////////////sNNNhmmdhNNyyyyydhs+//////////////////+++++++++++++++++++++++++++
y++++++++++++++++++++++++++++++++++yNNNhddhhmmyyyysoo++++++++++++++++++++++/////////////////////////
s++////////////////////////////////yNNmhdmhdmmyysysooo/////////+++//++//////////////////////////////
yoooooooooooooooooooooooooooooooooohNNNhdmmNmNhhhdysssoooooooooosooooooooooooooooooooooooooooooooooo

```

## Usage

To start using it, all you need is:
- Edit the .yaml file, specifying your CI steps;
- Past the .yaml file in your home directory;
- Run ciriema: `mvn clean package && java -jar target/quarkus-app/quarkus-run.jar`

### Learn it by example: The yaml file

```yaml
name: codereview-pipeline
sourceInfo:
  git:
    url: "https://github.com/ttzoutz/jenkin-devops-microservice.git" # Random project that I picked-up from the internet
    branch: master

steps:
  - name: compile
    runIn: shell
    commands:
      - mvn package
      - java -jar /Users/mrgurgel/apps/jacoco-0.8.7/lib/jacococli.jar report target/jacoco.exec --classfiles ./target/classes --html /tmp/jacoco-report
      - cat /tmp/jacoco-report/index.html
    postProcessors:
      - name: coverage
        spec:
          regexToExtractCurrentCoverageFromConsole: 'title="1" alt="1"\/><\/td><td class="ctr2" id="e1">(.*)%<\/td>'
          minimumPercentageAccepted: 80
```

For the example above, the console will show:
![Ciriema result](https://github.com/mrgurgel/ciriema/blob/main/src/main/docs/output-example.png?raw=true)
