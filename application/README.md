<img src="https://companieslogo.com/img/orig/MDB_BIG-ad812c6c.png?t=1648915248" width="50%" title="Github_Logo"/> <br>

# MongoDB Atlas Hands-on Training

### Nodejs 를 이용한 MongoDB CRUD
Nodejs로 Atlas 에 접속 하고 MongoDB Query 를 이용하여 데이터를 생성, 조회, 삭제를 테스트 합니다. 
NodeJS를 설치하고 테스트를 위해 관련 패키지를 설치 하여 줍니다.

````
% npm install

added 196 packages, and audited 197 packages in 2s

14 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
````
node_modules 폴더가 생성되어 관련된 라이브러리가 설치 됩니다.


#### Connection Test

MongoDB Atlas 와 연결을 위한 테스트 입니다.
connect.js 에 const uri을 수정 하여 줍니다.

````
const uri =mongodb+srv://atlas-account:<password>@cluster0.****.mongodb.net/myFirstDatabase?retryWrites=true&w=majority
````
연결 테스트를 위해 다음을 실행 합니다.

````
% node connect.js 
Connected successfully to server
````

#### Insert Test

MongoDB Atlas 와 연결하여 데이터를 생성 합니다.
insertOne.js 에 const uri을 수정 하여 줍니다.

````
const uri =mongodb+srv://atlas-account:<password>@cluster0.****.mongodb.net/myFirstDatabase?retryWrites=true&w=majority
````
입력할 데이터를 수정 하여 줍니다.

````
      const newUser = {
        ssn:"123-456-0001", 
        email:"user2@emailcom", 
        name:"Gildong Hong", 
        DateOfBirth: "1st Jan.", 
        Hobbies:["Martial arts"],
        Addresses:[{"Address Name":"Work","Street":"431, Teheran-ro GangNam-gu ","City":"Seoul", "Zip":"06159"}], 
        Phones:[{"type":"mobile","number":"010-5555-1234"}]
      };
````

입력 테스트를 위해 다음을 실행 합니다.

````
% node insertOne.js 
A document was inserted with the _id: 63bba1f8e554c42df82f974e
````
Atlas Console 에서 데이터 생성 여부를 확인 합니다.


#### find Test

MongoDB Atlas 와 연결하여 데이터를 조회 합니다.
findeOne.js 에 const uri을 수정 하여 줍니다.

````
const uri =mongodb+srv://atlas-account:<password>@cluster0.****.mongodb.net/myFirstDatabase?retryWrites=true&w=majority
````
입력할 데이터를 수정 하여 줍니다.
조회할 데이터의 ssn을 확인 합니다.  

`````
const query = {ssn:"123-456-7890"};
`````

데이터를 조회 합니다
````
% node findOne.js
Find One Record: 63ba34011dddaeaed894fc0e
Find One Record by SSN: 63ba34011dddaeaed894fc0e
````

#### Update Test


MongoDB Atlas 와 연결하여 데이터를 업데이트 합니다.
updateOne.js 에 const uri을 수정 하여 줍니다.

````
const uri =mongodb+srv://atlas-account:<password>@cluster0.****.mongodb.net/myFirstDatabase?retryWrites=true&w=majority
````
수정할 데이터를 ssn을 입력 하여 줍니다.
수정 대상 데이터의 ssn 및 수정할 데이터 항목을 확인 수정 하여 줍니다.
`````
const result = await userCollection.updateOne({"ssn":"123-456-7890"},{$set:{email:"kyudong.kim@mongodb.com"}});
      
`````

데이터를 수정 합니다
````
% node updateOne.js
1 document(s) matched the filter, updated 0 document(s)
````

#### Update Hobbies Test


MongoDB Atlas 와 연결하여 데이터를 업데이트 합니다.
updateHobbies.js 에 const uri을 수정 하여 줍니다.

````
const uri =mongodb+srv://atlas-account:<password>@cluster0.****.mongodb.net/myFirstDatabase?retryWrites=true&w=majority
````
수정할 데이터를 ssn을 입력 하여 줍니다.
수정 대상 데이터의 ssn 및 Hobby 항목을 추가 하여 줍니다. (취미로 Reading 추가 하기)
`````
const result = await userCollection.updateOne({"ssn":"123-456-7890"},{$push:{Hobbies:"Reading"}});
          
`````

데이터를 수정 합니다
````
node updateHobbies.js 
1 document(s) matched the filter, updated 1 document(s)
````
Atlas Data Console에서 데이터가 수정 된 것을 확인 합니다.


#### Remove Test


MongoDB Atlas 와 연결하여 데이터를 삭제 합니다.
removeUser.js 에 const uri을 수정 하여 줍니다.

````
const uri =mongodb+srv://atlas-account:<password>@cluster0.****.mongodb.net/myFirstDatabase?retryWrites=true&w=majority
````
삭제할 데이터를 수정 하여 줍니다.
삭제할 데이터의 ssn 및 입력 하여줍니다.
`````
const result = await userCollection.deleteOne({"ssn":"123-456-0001"});

`````

데이터를 삭제 합니다
````
% node removeUser.js 
1 document(s) removed
````
