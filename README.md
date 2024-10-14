2024-10-11

I've started up a Docker container with the ICE immunization service running. 

I created a basic input-message-populated.xml file based on the ICE instructions in the ICE Implementation Guides stored locally in this folder. 

I base 64 encoded that file and embedded it into sample-soap-ice-request.xml to create sample-soap-ice-request-with-data.xml. Using that I sent it to the local instance of Ice at POST http://localhost:8081/opencds-decision-support-service/evaluate with Header Content-Type application/soap+xml; charset=utf-8. That produces the response first-response.xml which appears to be a well-formed Ice response. In short, I installed and set up an instance of Ice and successfully sent it a request. 

Please refer also to my ChatGPT conversation titled ICE - US Immunization Decision Support Tools. 

Here's the [CDC IIS: HL7 Standard Code Set
Mapping CVX to Vaccine Groups](https://www2a.cdc.gov/vaccines/iis/iisstandards/vaccines.asp?rpt=vg). But that's not what ICE uses. 

See this [Google Sheet](https://docs.google.com/spreadsheets/d/1JB8QN2QeJACJmGdSkCaHr6LQ_8T942-J65Fjf_JDpic/edit?gid=2068558145#gid=2068558145) for all codes, including vaccine groups. 	The reference is [here](https://cdsframework.atlassian.net/wiki/spaces/ICE/pages/18972704/Downloads) and the master atlassian document is [here](https://cdsframework.atlassian.net/wiki/spaces). 

Here is the command to base64 encode a message:
```
base64 -i /Users/danheslinga/ice/{z}/ice-message-populated-{z}.xml -o /Users/danheslinga/ice/{z}/ice-message-encoded-{z}.txt
```
where `z` is an instance (test case) number. Test cases are in numbered folders in the root directory. For example, in the third test case:
```
base64 -i /Users/danheslinga/ice/3/ice-message-populated-3.xml -o /Users/danheslinga/ice/3/ice-message-encoded-3.txt
```

To decode the base64 returned message:
```
echo "your_base64_string" | base64 -d -o path/to/output/file.xml
```
like
```
echo "PD94bWwgdmVy...{truncated}" | base64 -d -o /Users/danheslinga/ice/3/ice-response-message-decoded-3.xml
```