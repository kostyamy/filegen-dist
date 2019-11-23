# Filegen
The filegen is an applicaiton to help you generate template based data file(s) often used in testing.  
The application is written in C# using .Net Core 2.x framework and runs on on whatever platform .NET Core supports.

## How to run:
```powershell
>dotnet filegen.dll "begin=<file path>" "<repeat>=<template file>" .... "end=<file path>" "output.xml" 
- "begin" template file inserted at the beginning of the output file
- "<repeat>=<file path>" template file(s) used to create body of the output file 
  when template file extension is omitted the '.xml' extension is assumed
- "end=<file path>" template file appended to the end of the output file
- last parameter is a file path of the output file
```

## Example:
```powershell
> dotnet filegen.dll "begin=templates\begin.xml" "100=templates\doc1.xml" "200=templates\doc2.xml" "end=templates\end.xml" "output.xml" 
```
Explanation of the example:
1. in current directory create file "output.xml"
2. append content of the templates\begin.xml template at the beginning of the output.xml file
3. in random order insert 100 records of "templates\doc1.xml" and 200 records of "templates\doc2.xml" files
4. when all 300 records insrted append the template\end.xml to the end of the output.xml file

## Terminology
* Template - text file used specified number of times in ramdon order to generate final output file. Teher is not limnation of actual file format of the template file but normally it's of one of the following: xml, json, sql, txt, or csv.
* Variable - built-in variable name used in expressions with a template file (including the begin and the end) to perform substibution
 Variables can be used as-is using default formatting or optionally you can specify format of the value.
 Formatting depends on variable type (like guid vs. integer vs. date, etc.) and uses .Net's formatting mechanism.
* Function - simular to variable functions are built-in features used within template to perform action along with possible substibution
* Record - instance of a template file in the generation process.

## Template parameters
```
	${copyFile:source,destination} - copy file overwriting the desctination
	${appendFile:file,text} - appends text a file
	${writeFile:file,text} - writes text a file
```

## Variables
Within template file you can use the following built-in variables:
```
	${globalId1:format}  \
	${globalId2:format}   -> guids assigned at the beginning of the run
	${globalId3:format}  /

	${globalNum1:format} \
	${globalNum2:format}  -> random integers assigned at the beginning of the run
	${globalNum3:format} /

	${index:format}  - 0 based record index
	${number:format} - 1 based record number

	${id1:format}  \
	${id2:format}   -> guids generated for each record
	${id3:format}  /

	${num1:format} \
	${num2:format}  -> random integers generated for each record
	${num3:format} /
	
    ${today:format} - today's date and time
	${date} - today's date (mm/dd/yyyy)
	${yyyy} - today's year
	${mm} - today's month
	${month} - name of today's month
	${time} - today's time (hh:mm:ss)
	${ticks:format} - current time ticks
```
## Formats
### Guild formats:
* D - "xxx-xxx-xxxxx---"
* B - "xxx-xxx-xxxxx---"
* N - "xxx-xxx-xxxxx---"
### Numeric formats:
 still working ...
### Date formats
still working ...

## Functions
Within template file you can use the following built-in functions:
```
still working ...
```
