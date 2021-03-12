Context
==========================================
RandomUserData / User
------------------------------------------

* 앱 내에서 전역적으로 사용할 데이터를 정의함.
* 타입스크립트 사용 시
  
### 1. User/@types/index.d.ts 파일
```typescript
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
### 2. User/index.tsx 파일

#### 1) defaultContext
```typescript
const defaultContext : IUserContext = {
    isLoading : false,
    userInfo : undefined,
    login : (email : string, passwrod : string) => {},
    getUserInfo : () => {},
    logout : () => {},
}

const UserContext = createContext(defaultContext);

interface Props {
    children : JSX.Elemetn | array<JSX.Element>;
}
```

#### 2) UserContextProvider : useState, useEffect 사용
```typescript
const UserCOntextProvider = ({children} : Props) => {
    const [userInfo, setUserInfo] = useState<IUserInfo | undefined>(undefined);
    const [isLoading, setIsLoading] = useState<boolean>(false);

    const login = (email : string, password : string) : void => {
        //로그인 정보 체크 추가
        //토큰 확인 추가
        AsyncStorage.setItem('token', 'save your token').then(() => {
            setUserInfo({
                name : 'dev',
                email : 'dev@test.com'
            });
            setIsLoading(true);
        });        
    };

    const getUserInfo = () : void => {
        AsyncStorage.getItem('token')
            .then(value => {
                if (value) {
                    setUserInfo({
                        name : 'dev',
                        email : 'dev@test.com'
                    });
                }
                setIsLoading(true);
            })
            .catch(() => {
                setUserInfo(undefined);
                setIsloading(true);
            });
    };

    const logout = () : void => {
        AyncStorage.removeItem('token');
        setUserInfo(undefined);
    };

    useEffect(() => {
        getUserInfo();
    }, []);

    return (
        <UserContext.Provider
            value={{
                isLoading,
                userInfo,
                login,
                getUserInfo,
                logout,
            }}
        >
            {children}
        </UserContext.Provider>
    );
};

export {UserContextProvide, UserContext};
```


