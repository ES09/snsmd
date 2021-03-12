Context
==========================================
RandomUserData / User
------------------------------------------

* 앱 내에서 전역적으로 사용할 데이터를 정의함.
* 타입스크립트 사용 시
  
### 1. User/@types/index.d.ts 파일
```
interface IUserInfo {
    name : string;
    email : string;
}

interface IUserContext {
    isLoading : boolean;
    userInfo : IUserInfo | undefined;
    login : (email : string, password : string) => void;
    getUserInfo : () => void;
    logout : () => void; 
}
```