![image](https://github.com/AbdullahSGF/BlackHatMEA-Qualifications-CTF/assets/131845686/b4f8b033-fd5d-4dd2-a929-ead0663ea4b6)
 
After downloading the file we will see an image and from the description of the challenge we can assure that the image contains something.


![image](https://github.com/AbdullahSGF/BlackHatMEA-Qualifications-CTF/assets/131845686/a9eebd13-8aa7-4d1d-bbb2-1c7c3a34fa51)

So let's try to read the metadata of it using exiftool.


![image](https://github.com/AbdullahSGF/BlackHatMEA-Qualifications-CTF/assets/131845686/5962233b-26ef-487a-ae57-70df799bd5b0)

 
After running exiftool we noticed a link attached in the comment section.


![image](https://github.com/AbdullahSGF/BlackHatMEA-Qualifications-CTF/assets/131845686/c049c387-dc55-4aac-9c0e-61d6315288ad)

 
Following that link will lead us to a website.


![image](https://github.com/AbdullahSGF/BlackHatMEA-Qualifications-CTF/assets/131845686/3a384196-4fe1-4ea6-9514-e101a33d49b9)


At first people thought this is an OSINT challenge, but we can in the bottom it says find more data somewhere here. So how we can find more data in this page? We can see that the website is running from a github repository.


![image](https://github.com/AbdullahSGF/BlackHatMEA-Qualifications-CTF/assets/131845686/12122fe8-1811-424e-88f3-881cf294f093)

Let’s try to search for it in github.


 ![image](https://github.com/AbdullahSGF/BlackHatMEA-Qualifications-CTF/assets/131845686/44c711e8-577e-4114-a0ce-e7435787647b)

 


 
After we found we can see there is a file called fulldata, and that file contains a Pastebin link says more data.


 ![image](https://github.com/AbdullahSGF/BlackHatMEA-Qualifications-CTF/assets/131845686/5b6085ac-8600-452a-bedb-ea2d334ae1a5)

 
 ![image](https://github.com/AbdullahSGF/BlackHatMEA-Qualifications-CTF/assets/131845686/25c6f810-2c01-4763-bc20-a58a669592cd)


When we opened the link we can see many websites and user credentials belongs to it but remember the note in the github page it says only one password is working. So we first tried the mega link because it contains a file which is more attractive.


![image](https://github.com/AbdullahSGF/BlackHatMEA-Qualifications-CTF/assets/131845686/1ba0c990-1991-49f3-a49c-f5a5eaeffcf2)

 
We have tried the password give in the Pastebin and it worked.


 ![image](https://github.com/AbdullahSGF/BlackHatMEA-Qualifications-CTF/assets/131845686/d9e920fd-8c2a-426f-8a2d-acb1f71a45b5)

 
![image](https://github.com/AbdullahSGF/BlackHatMEA-Qualifications-CTF/assets/131845686/e6f2a4b0-f154-49db-8986-c6357e679ed8)


 
After opening the file we have noticed that the file is a Google chrome profile folder, that means it contains everything he did in google chrome including the search history and visited links.


![image](https://github.com/AbdullahSGF/BlackHatMEA-Qualifications-CTF/assets/131845686/dfbf9d07-fc26-4719-8f51-01b103c1dcba)


So let’s navigate to Default folder which is contains the most important information.


 ![image](https://github.com/AbdullahSGF/BlackHatMEA-Qualifications-CTF/assets/131845686/36a3b237-ae78-4568-815b-cbc35c8a3209)

 ![image](https://github.com/AbdullahSGF/BlackHatMEA-Qualifications-CTF/assets/131845686/cbff5031-5e69-4536-abad-a5ea0eb8c93a)
 

Usually when we investigate a browser profile folder the first thing we do is to go to History database file (DB) or any DB files in general, but in this challenge we haven’t find anything suspicious in them. So I remembered the challenge name which is “Extended” so it has something to do with the Extensions. Let’s check the Extensions file.
![image](https://github.com/AbdullahSGF/BlackHatMEA-Qualifications-CTF/assets/131845686/ca6cd454-8dad-4711-83e9-e10c7235f999)

![image](https://github.com/AbdullahSGF/BlackHatMEA-Qualifications-CTF/assets/131845686/9b54162b-6de0-4f3d-a1dd-e7bcf2776a1f)

 
 
As we can see there are many extensions, so I have checked each of them and nothing was found until we opened this extension.

![image](https://github.com/AbdullahSGF/BlackHatMEA-Qualifications-CTF/assets/131845686/9db366db-a91d-42d6-8045-883c1099fa14)

![image](https://github.com/AbdullahSGF/BlackHatMEA-Qualifications-CTF/assets/131845686/f6de1a7e-8ab7-43c9-b7d0-f84c1594e7c6)


 
We can see two folders the manifest and service-worker.js
The manifest folder it’s only contains an information about the extension. So we opened service-worker.js.

![image](https://github.com/AbdullahSGF/BlackHatMEA-Qualifications-CTF/assets/131845686/4c96f331-85f7-4cf8-b350-f4d08752dc6b)

 
After opening the code in notepad we can see this is an obfuscated JavaScript code which is very suspicious!

So I have used this online tool to deobfuscate it.
https://deobfuscate.io/

![image](https://github.com/AbdullahSGF/BlackHatMEA-Qualifications-CTF/assets/131845686/ba8a2c39-8b65-4a0b-a138-094d5c6ef95f)

 

Let’s copy the results and paste it back to our notepad.
After analyzing the code we can see a functions called connect.

![image](https://github.com/AbdullahSGF/BlackHatMEA-Qualifications-CTF/assets/131845686/6e41cd01-8b0b-48c4-ba85-1dfe3c3548ef)

 
This functions will generate a link to connect to a websocket and this isn’t the only suspicious part!

The function will sum the values of theese variables in a reversed order from right to left.
The result will be 

wss://Qf2MjYwAzNyIDOjVTZkJTY---1QjY0YGNxEDM1cTMxQ2YjV---WYwIjYzMTM2sXWHFETGhkQ.oast.pro/


![image](https://github.com/AbdullahSGF/BlackHatMEA-Qualifications-CTF/assets/131845686/86599546-bd2c-4bc2-9cf6-89d307aa84f6)


Before we try to connect to the WebSocket haven’t you noticed something suspicious in this link? Yes it’s a base64 ! Let’s try to decode it first using CyberChef.

https://gchq.github.io/CyberChef/


 ![image](https://github.com/AbdullahSGF/BlackHatMEA-Qualifications-CTF/assets/131845686/5aff97f4-4d5c-4e70-b9a3-340800518708)


That is very disappointing results but wait! Remember that the order of that function was reversed so let’s try to reverse it first then decode it.


![image](https://github.com/AbdullahSGF/BlackHatMEA-Qualifications-CTF/assets/131845686/9705c6ce-42d9-4d65-8181-fd186cdcae1f)

 

Finally we got it! Here is your flag happy hacking (:
BHFLAGY{6133b20aeccd11750114f4b45a2de5c822700b36}


